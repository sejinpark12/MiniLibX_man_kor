# MiniLibX

## NAME
MiniLibX - 이미지 조작하기

## SYNOPSYS
```c
void *
mlx_new_image(void *mlx_ptr, int width, int height);

char *
mlx_get_data_addr(void *img_ptr, int *bits_per_pixel, int *size_line, int *endian);

int
mlx_put_image_to_window(void *mlx_ptr, void *win_ptr, void *img_ptr, int x, int y);

unsigned int
mlx_get_color_value(void *mlx_ptr, int color);

void *
mlx_xpm_to_image(void *mlx_ptr, char **xpm_data, int *width, int *height);

void *
mlx_xpm_file_to_image(void *mlx_ptr, char *filename, int *width, int *height);

int
mlx_destroy_image(void *mlx_ptr, void *img_ptr);
```

## DESCRIPTION
`mlx_new_image()`는 메모리에 새로운 이미지를 생성합니다.

이 함수는 나중에 이미지를 조작하기 위해 필요한 `void *` 식별자를 반환합니다.

이미지를 생성하기 위해서는 `width`와 `height` 파라미터를 사용하는 이미지 크기가 필요합니다. `mlx_ptr`은 연결 식별자입니다([mlx man page](https://github.com/psj3205/MiniLibX_man_kor/blob/main/mlx.md)를 보십시오).

사용자는 이미지 안에 그릴 수 있습니다([아래 확인]()). 그리고 언제든지 특정 윈도우 안에 이미지를 덤프하여 화면에 표시할 수 있습니다.

`mlx_put_image_to_window()`를 사용하여 이 작업을 수행할 수 있습니다.

세 가지 식별자가 디스플레이에 연결, 윈도우 사용, 이미지(각각 `mlx_ptr`, `win_ptr`, `img_ptr`)를 위해 필요합니다. `(x, y)` 좌표는 윈도우 안에서 이미지가 위치할 곳을 정의합니다.

`mlx_get_data_addr()`은 생성된 이미지에 대한 정보를 반환하며, 나중에 사용자가 수정할 수 있습니다.

`img_ptr` 파라미터는 사용할 이미지를 지정합니다.

다음 3개의 파리미터는 3개의 서로 다른 유효한 정수의 주소입니다.

`bit_per_pixel`은 픽셀의 색상을 나타는데 필요한 비트의 수로 채워집니다(색 깊이(depth of the image)라고도 불립니다).

`size_line`은 메모리 안에서 이미지 한 줄을 저장하는 바이트의 수입니다. 이 정보는 이미지의 한 줄에서 다른 줄로 이동하는데 필요합니다.

## STORING COLOR INSIDE IMAGES

## XPM IMAGES

## RETURN VALUES

## SEE ALSO
mlx(3), mlx_new_window(3), mlx_pixel_put(3), mlx_loop(3)

## AUTHOR
Copyright ol@ - 2002-2015 - Olivier Crouzet
