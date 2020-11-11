# MiniLibX

## NAME
MiniLibX - 윈도우 관리

## SYNOPSYS
```c
void *
mlx_new_window(void *mlx_ptr, int size_x, int size_y, char *title);

int
mlx_clear_window(void *mlx_ptr, void *win_ptr);

int
mlx_destroy_window(void *mlx_ptr, void *win_ptr);
```

## DESCRIPTION
`mlx_new_window()` 함수는 화면의 크기를 결정하는 `size_x`와 `size_y` 파라미터를 사용하여 화면에 새로운 윈도우를 생성합니다. `title` 파라미터는 윈도우의 타이틀 바에 표시되는 텍스트입니다.

`mlx_ptr` 파라미터는 `mlx_init()`으로부터 반환받은 연결 식별자입니다([mlx man page](https://github.com/psj3205/MiniLibX_man_kor/blob/main/mlx.md)를 보십시오). `mlx_new_window()`는 다른 MiniLibX 호출에 사용되는 `void *` 윈도우 식별자를 반환합니다.

MiniLibX는 임의의 수의 개별 윈도우를 처리할 수 있음을 주목하십시오.

`mlx_clear_window()`와 `mlx_destroy_window()`는 주어진 윈도우에 대해 각각 clear와 destroy를 수행합니다. 두 함수 모두 동일한 파라미터를 가지고 있습니다: `mlx_ptr`은 화면 연결 식별자이고 `win_ptr`은 윈도우 식별자입니다.

## RETURN VALUES
`mlx_new_window()`가 새로운 윈도우 생성을 실패(어떤 이유로든)할 경우, `NULL`을 반환합니다. 성공할 경우, `NULL`이 아닌 포인터가 윈도우 식별자로 반환됩니다. `mlx_clear_window`와 `mlx_destroy_window`는 당장 아무것도 반환하지 않습니다.

## SEE ALSO
[mlx(3)](https://github.com/psj3205/MiniLibX_man_kor/blob/main/mlx.md), [mlx_pixel_put(3)](https://github.com/psj3205/MiniLibX_man_kor/blob/main/mlx_pixel_put.md), mlx_new_image(3), mlx_loop(3)

## AUTHOR
Copyright ol@ - 2002-2015 - Olivier Crouzet
