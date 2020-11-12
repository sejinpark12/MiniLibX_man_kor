# MiniLibX

## NAME
MiniLibX - 이미지 조작하기

## SYNOPSYS
```c
void *
mlx_new_image(void *mlx_ptr, int width, int height);

char *
mlx_get_data_addr(void *img_ptr, int *bits_per_pixel, int *size_line, int *endian);

int
mlx_put_image_to_window(void *mlx_ptr, void *win_ptr, void *img_ptr, int x, int y);

unsigned int
mlx_get_color_value(void *mlx_ptr, int color);

void *
mlx_xpm_to_image(void *mlx_ptr, char **xpm_data, int *width, int *height);

void *
mlx_xpm_file_to_image(void *mlx_ptr, char *filename, int *width, int *height);

int
mlx_destroy_image(void *mlx_ptr, void *img_ptr);
```

## DESCRIPTION
`mlx_new_image()`는 메모리에 새로운 이미지를 생성합니다. 이 함수는 나중에 이미지를 조작하기 위해 필요한 `void *` 식별자를 반환합니다. 이미지를 생성하기 위해서는 `width`와 `height` 파라미터를 사용하는 이미지 크기가 필요합니다. `mlx_ptr`은 연결 식별자입니다([mlx man page](https://github.com/psj3205/MiniLibX_man_kor/blob/main/mlx.md)를 보십시오).

사용자는 이미지 안에 그릴 수 있습니다([아래 확인]()). 그리고 언제든지 특정 윈도우 안에 이미지를 덤프하여 화면에 표시할 수 있습니다. `mlx_put_image_to_window()`를 사용하여 이 작업을 수행할 수 있습니다. 세 가지 식별자가 디스플레이에 연결, 윈도우 사용, 이미지(각각 `mlx_ptr`, `win_ptr`, `img_ptr`)를 위해 필요합니다. `(x, y)` 좌표는 윈도우 안에서 이미지가 위치할 곳을 정의합니다.

`mlx_get_data_addr()`은 생성된 이미지에 대한 정보를 반환하며, 나중에 사용자가 수정할 수 있습니다. `img_ptr` 파라미터는 사용할 이미지를 지정합니다. 다음 3개의 파리미터는 3개의 서로 다른 유효한 정수의 주소입니다. `bits_per_pixel`은 픽셀의 색상을 나타는데 필요한 비트의 수로 채워집니다(색 깊이(depth of the image)라고도 불립니다). `size_line`은 메모리 안에서 이미지 한 줄을 저장하는 바이트의 수입니다. 이 정보는 이미지의 한 줄에서 다른 줄로 이동하는데 필요합니다. `endian`은 이미지의 픽셀 색상을 little `(endian == 0)` 또는 big `(endian == 1)`에 저장해야하는지 여부를 의미합니다.

`mlx_get_data_addr`은 이미지가 저장되어 있는 메모리의 시작 지점을 나타내는 `char *`형 주소를 반환합니다. 이 주소로부터, 첫 번째 `bits_per_pixel` 비트는 이미지에서 첫 번째 줄의 첫 번째 픽셀 색상을 나타냅니다. 두 번째 `bits_per_pixel` 비트는 첫 번째 줄의 두 번째 픽셀을 나타냅니다. 나머지도 마찬가지입니다. 주소에 `size_line`을 추가하여 두 번째 줄의 시작 부분을 가져옵니다. 이와 같은 방식으로 이미지의 어떤 픽셀에 접근이 가능합니다.

`mlx_destroy_image`는 주어진 이미지(`img_ptr`)를 파괴합니다.

## STORING COLOR INSIDE IMAGES
디스플레이에 따라, 픽셀 색을 저장하는데 필요한 비트 수는 변경할 수 있습니다. 사용자는 주로 RGB 모드로 색상을 나타냅니다. RGB 모드는 각 성분으로 한 바이트를 사용합니다([mlx_pixel_put man page](https://github.com/psj3205/MiniLibX_man_kor/blob/main/mlx_pixel_put.md)를 보십시오). 이미지의 bits_per_pixel 요구사항에 맞게 변환되어야 하며, 그래픽 시스템이 이해할 수 있는 색상을 만들어야 합니다. 이것이 `mlx_get_color_value()` 함수의 목적입니다. 표준 RGB 색상 파라미터를 받고, unsiged int 값을 반환합니다. 이 값의 `bits_per_pixel` 최하위 비트는 이미제에 저장될 수 있습니다.

최하위 비트 위치는 로컬 컴퓨터의 엔디안을 따른다는 것을 명심하십시오. 이미지의 엔디안이 로컬 엔디안과 다르다면, 사용하기 전에 값을 변환해야 합니다.

## XPM IMAGES
`mlx_xpm_to_image()`와 `mlx_xpm_file_to_image()` 함수는 동일한 방식으로 새로운 이미지를 생성합니다. 사용하는 함수에 따라, `xpm_data` 또는 `filename`을 파라미터로 사용합니다. MiniLibX는 xpm 이미지를 처리하는 표준 Xpm 라이브러리를 사용하지 않습니다. xpm 이미지의 모든 유형을 읽지 못할 수 있습니다. 하지만, 투명도는 처리할 수 있습니다.

## RETURN VALUES
이미지를 생성하는 `mlx_new_image()`, `mlx_xpm_to_image()`, `mlx_xpm_file_to_image()` 세 가지 함수는 오류가 발생할 경우 `NULL`을 반환합니다. 성공할 경우, 이미지 식별자로 `NULL`이 아닌 포인터를 반환합니다.

## SEE ALSO
[mlx(3)](https://github.com/psj3205/MiniLibX_man_kor/blob/main/mlx.md), [mlx_new_window(3)](https://github.com/psj3205/MiniLibX_man_kor/blob/main/mlx_new_window.md), [mlx_pixel_put(3)](https://github.com/psj3205/MiniLibX_man_kor/blob/main/mlx_pixel_put.md), mlx_loop(3)

## AUTHOR
Copyright ol@ - 2002-2015 - Olivier Crouzet

