# MiniLibX

## NAME
MiniLibX - 학생들을 위한 간단한 그래픽 인터페이스 라이브러리

## SYNOPSYS
```c
#include <mlx.h>

void *
mlx_init();
```

## DESCRIPTION
MiniLibX는 X-Window/Cocoa 프로그래밍 지식 없이, 그래픽 소프트웨어를 생성할 수 있는 쉬운 방법입니다. 간단한 윈도우 생성, 드로링 툴, 이미지, 기본 이벤트 관리를 제공합니다.

## BSD/LINUX X-WINDOW CONCEPT
X-Window는 유닉스용 네트워크 오리엔티드 그래픽 시스템입니다. X-Window는 두 가지 주요 파트로 구성되어 있습니다:
첫 번째 파트, 당신의 소프트웨어는 화면에 어떤것을 그리길 원합니다. 그리고/또는 키보드 & 마우스 입력을 받습니다.
두 번째 파트, X-Server는 화면, 키보드, 마우스를 관리합니다(종종 "디스플레이"라고 불립니다).

그리기 명령(소프트웨어에서 X-Server로)과 키보드/마우스 이벤트(X-Server에서 소프트웨어로)를 전송하기 위해서는 두 엔티티 간에 네트워크 연결이 설정되어야 합니다.

## MACOSX CONCEPT
MaxOSX 운영체제는 화면(또는 "디스플레이")상의 그래픽 접근을 처리합니다.
첫 번째 파트, 당신의 소프트웨어는 화면에 어떤것을 그리길 원합니다. 그리고/또는 키보드 & 마우스 입력을 받습니다.
두 번째 파트, 화면, 윈도우 시스템, 키보드, 마우스를 처리하는 MaxOSX 내부의 그래픽 프레임워크
이 두 엔티티간의 연결이 설정되어야 합니다.

## INCLUDE FILE
MiniLibX API를 올바르게 사용하기 위해서는 mlx.h를 인클루드해야 합니다. mlx.h는 단지 함수들의 프로토타입만을 포함하고 있고 구조체가 필요하지 않습니다.

## LIBRARY FUNCTIONS
우선, 당신의 소프트웨어와 화면 간의 연결을 초기화해야 합니다. 한 번 연결이 설정되면, 그래픽 명령을 전송하기 위한 MiniLibX 다른 함수들을 사용할 수 있습니다. 예를 들어 "이 윈도우의 노란색 픽셀을 그리고 싶어" 또는 "사용자가 키를 눌렸나?".

`mlx_init` 함수는 소프트웨어와 화면 간의 연결을 생성합니다. 파라미터는 필요없고, 라이브러리 루틴에 대한 추가 호출에 사용되는 void * 식별자를 반환합니다.

모든 다른 MiniLibX 함수들은 다음의 man 페이지에 설명되어 있습니다:

	- [mlx_new_window](https://github.com/psj3205/MiniLibX_man_kor/blob/main/mlx_new_window.md) : 윈도우 관리
	- [mlx_pixel_put](https://github.com/psj3205/MiniLibX_man_kor/blob/main/mlx_pixel_put.md) : 윈도우에 그리기
	- mlx_new_image : 이미지 조작
	- mlx_loop : 키보드/마우스 이벤트 처리

## LINKING MiniLibX on BSD/Linux and X-Window
MiniLibX 함수를 사용하기 위해서는 MiniLibX 라이브러리를 포함하여 몇가지 라이브러리를 당신의 소프트웨어에 링크시켜야 합니다. 이 작업을 하기 위해서, 간단히 다음의 인자들을 링크할 때 추가합니다:

`-lmlx -lXext -lX11`

`-L` 플래그를 사용하여 이 라이브러리들의 경로를 지정해주어야 합니다.

## LINKING MiniLibX on MACOSX
MiniLibX 함수를 사용하기 위해서는 MiniLibX 라이브러리와 몇가지 시스템 프레임워크를 당신의 소프트웨어에 링크시켜야 합니다:

`-lmlx -framework OpenGL -framework Appkit`

`-L` 플래그를 사용하여 MiniLibX 라이브러리 경로를 지정해주어야 합니다.

## RETURN VALUES
`mlx_init()` 이 그래픽 시스템 연결을 실패할 경우, `NULL`이 반환됩니다. 성공할 경우, `NULL`이 아닌 포인터가 연결 식별자로 반환됩니다.

## SEE ALSO
[mlx_new_window(3)](https://github.com/psj3205/MiniLibX_man_kor/blob/main/mlx_new_window.md), [mlx_pixel_put(3)](https://github.com/psj3205/MiniLibX_man_kor/blob/main/mlx_pixel_put.md), [mlx_new_image(3)](https://github.com/psj3205/MiniLibX_man_kor/blob/main/mlx_new_image.md), [mlx_loop(3)](https://github.com/psj3205/MiniLibX_man_kor/blob/main/mlx_loop.md)

## AUTHOR
Copyright ol@ - 2002-2015 - Olivier Crouzet
