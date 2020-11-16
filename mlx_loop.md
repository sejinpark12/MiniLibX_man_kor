# MiniLibX

## NAME
MiniLibX - 이벤트 처리하기

## SYNOPSYS
```c
int
mlx_loop(void *mlx_ptr);

int
mlx_key_hook(void *win_ptr, int (*funct_ptr)(), void *param);

int
mlx_mouse_hook(void *win_ptr, int (*funct_ptr)(), void *param);

int
mlx_expose_hook(void *win_ptr, int (*funct_ptr)(), void *param);

int
mlx_loop_hook(void *mlx_ptr, int (*funct_ptr)(), void *param);
```

## EVENTS
X-Window와 MacOSX의 그래픽 시스템은 양방향적입니다. 한 쪽에서는, 프로그램이 픽셀, 이미지 등을 스크린에 출력하기 위한 명령을 보냅니다. 다른 쪽에서는, 스크린에 연동된 키보드나 마우스로부터 정보를 받을 수 있습니다. 이러한 동작을 통해 프로그램은 키보드나 마우스로부터 "이벤트"를 수신합니다.

## DESCRIPTION
이벤트를 수신하려면 `mlx_loop()`을 사용해야만 합니다. 이 함수는 반환값이 없습니다. 그리고 이 함수는 이벤트 수신을 기다린 다음 해당 이벤트와 연동된 사용자 정의 함수를 호출하는 무한 반복문입니다. 연결 식별자 mlx_ptr이라는 한 개의 매개변수가 필요합니다([mlx man page](https://github.com/psj3205/MiniLibX_man_kor/blob/main/mlx.md)를 보십시오).

다음 세 가지의 이벤트에 대한 서로 다른 함수들을 할당할 수 있습니다.
  - 키 누름
  - 마우스 버튼 누름
  - 윈도우의 일부를 다시 그려야 함("expose" 이벤트라고 불리는 이것을 처리하는 것은 프로그램의 역할)

각각의 윈도우는 동일한 이벤트에 대해 서로 다른 함수를 정의할 수 있습니다.

세 함수 `mlx_key_hook()`, `mlx_mouse_hook()`, `mlx_expose_hook()`는 완전히 동일하게 작동합니다. `funct_ptr`은 이벤트가 발생할 경우, 호출하고자 하는 함수의 포인터입니다. 이 할당은 `win_ptr` 식별자에 의해 정의된 윈도우에만 적용됩니다. `param` 주소는 함수가 호출될 때마다 항상 함수에 전달되고, 필요한 매개변수를 저장하는데 사용됩니다.

mlx_loop_hook() 함수의 구문은 위에서 보았던 이전 함수들과 동일하지만, 이벤트가 발생하지 않을 때 매개변수로 주어진 함수가 호출됩니다.

이벤트를 수신했을 때, MiniLibX는 다음의 고정 매개변수 함수를 호출합니다.
  - expose_hook(void *param);
  - key_hook(int keycode, void *param);
  - mouse_hook(int button, int x, int y, void *param);
  - loop_hook(void *param);

이 함수명들은 임의적입니다. 여기서는 이벤트에 따라 파라미터를 구분하기 위해서 사용됩니다. 이 함수들은 MiniLibX의 **일부분이 아닙니다.**

`param`은 `mlx_*_hook` 호출을 지정하는 주소입니다. 이 주소는 MiniLibX에서 사용되거나 수정되지 않습니다. 키와 마우스 이벤트는 추가 정보가 전달됩니다: `keycode`는 어떤 키가 입력되었는지 나타냅니다(X11 : "keysymdef.h" 헤더파일을 살펴보십시오, MacOS : 작은 프로그램을 만들어서 직접 알아내십시오.) `(x, y)`는 윈도우 안의 마우스 클릭 좌표입니다. `button`은 어떤 마우스 버튼을 입력했는지를 나타냅니다.

## GOING FURTHER WITH EVENTS
MiniLibX는 모든 타입의 이벤트에 대한 더 일반적인 접근을 제공합니다. `mlx.h` 는 `mlx_*_hook` 함수와 동일한 방식으로 동작하는 `mlx_hook()`의 정의를 포함하고 있습니다. 이벤트와 마스크 값은 X11 인클루드 파일 "X.h"에서 가져옵니다. (호환성 목적으로 MacOSX에서도 )

어떻게 MiniLibX가 특정 이벤트에 대한 사용자 정의 함수를 호출하는지 알고 싶다면 mlx_int_param_event.c의 소스 코드를 살펴보십시오.

## SEE ALSO
[mlx(3)](https://github.com/psj3205/MiniLibX_man_kor/blob/main/mlx.md), [mlx_new_window(3)](https://github.com/psj3205/MiniLibX_man_kor/blob/main/mlx_new_window.md), [mlx_pixel_put(3)](https://github.com/psj3205/MiniLibX_man_kor/blob/main/mlx_pixel_put.md), [mlx_new_image(3)](https://github.com/psj3205/MiniLibX_man_kor/blob/main/mlx_new_image.md)

## AUTHOR
Copyright ol@ - 2002-2015 - Olivier Crouzet
