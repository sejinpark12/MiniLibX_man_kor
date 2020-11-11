# MiniLibX

## NAME
MiniLibX - 윈도우 내부 그리기

## SYNOPSYS
```c
int
mlx_pixel_put(void *mlx_ptr, void *win_ptr, int x, int y, int color);

int
mlx_string_put(void *mlx_ptr, void *win_ptr, int x, int y, int color, char *string);
```

## DESCRIPTION
`mlx_pixel_put()` 함수는 `(x ,y)`좌표와 특정 색을 사용하여 `win_ptr` 윈도우 안에 정의된 픽셀을 그립니다.

원점 `(0, 0)`은 윈도우의 왼쪽 상단이고, x좌표와 y좌표는 각각 오른쪽과 아래쪽으로 향합니다.

연결 식별자 `mlx_ptr`이 필요합니다([mlx man page](https://github.com/psj3205/MiniLibX_man_kor/blob/main/mlx.md)를 보십시오).

`mlx_string_put()`은 `mlx_pixel_put()`과 동일한 의미의 파라미터를 가지고 있습니다. 단순한 픽셀 대신에, 특정 문자열이 `(x, y)`에 표시됩니다.

두 함수 모두, 지정된 윈도우 밖에서는 아무것도 표시할 수 없고, 선택된 윈도우 앞에 다른 윈도우를 표시할 수 없습니다.

## COLOR MANAGEMENT
color 파라미터는 정수형 타입을 가지고 있습니다.

표시 색상은 아래에 정의된 구조의 정수로 인코딩이 필요합니다.

모든 표시가능한 색상은 세 가지 기본 색으로 나눌 수 있습니다: red, green and blue.

0-255 범위의 3개의 값은 원본 색을 만드는데 각각의 색이 얼마나 혼합되는지를 나타냅니다. 정수의 최하위 바이트 3개는 아래의 그림처럼 채워집니다.

```
	| 0 | R | G | B |    color integer
	+---+---+---+---+
```

정수를 채우는 동안, 엔디안 문제를 피해야합니다. "blue" 바이트는 항상 최하위 바이트여야 합니다.


## SEE ALSO
[mlx(3)](https://github.com/psj3205/MiniLibX_man_kor/blob/main/mlx.md), [mlx_new_window(3)](https://github.com/psj3205/MiniLibX_man_kor/blob/main/mlx_new_window.md), mlx_new_image(3), mlx_loop(3)

## AUTHOR
Copyright ol@ - 2002-2015 - Olivier Crouzet
