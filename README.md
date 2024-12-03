# RGBA_TexturePacker
TexturePacking Tool


유니티, 언리얼, Godot와 같은 게임 엔진에서 사용할 여러 개의 텍스처를 하나의 텍스처로 합치는 툴입니다.
(메탈릭 맵, 러프니스 맵, 앰비언트 오쿨루전(AO) 맵, 디테일 마스크 맵)


일단 전 3D 전문 아티스트는 아닙니다. 하지만 3D를 활용할 일은 종종 있습니다.


유니티 urp의 기본 litShader 메테리얼과 hdrp의 마스크맵은
텍스처의 R채널에서 메탈릭 맵, G채널에서 AO 맵, B채널에서 디테일 마스크,
A에서 스무스니스 맵을 추출합니다.

**(R : Metallic, G: AO, B : Detail Mask, A : Smoothness)**


**스무스니스 맵은 러프니스 맵을 반전시킨 결과물로 유니티에서만 사용합니다.**


하지만 섭스턴스 페인터를 사용하지 않는 상황에서 스무스니스맵을 위해 포토샵에서 알파 채널 작업을 하고, 이미지를 반전시키는 과정은 너무 귀찮아서
해당 툴을 제작하게 되었습니다.


저는 언리얼은 사용하지 않기에 제가 설정한 언리얼 프리셋이 실제로 정확할지는 모르겠지만, 여러분이 원하는 대로 배치해서 패킹해도 큰 문제는 없을 것입니다.
현재 세팅된 값은 **(R : AO, G: Roughness, B: Metallic)**


Godot엔진도 Unreal과 같은 세팅을 사용하면 좋을 것 같습니다.



---
다음과 같은 점만 주의하면 됩니다.


1. 투명도가 적용된 png는 소스로 사용하지 않는다. (예기치 않은 결과물이 나올 수 있음)
2. RGB 텍스쳐 칸이 아닌 곳에는 흑백 데이터 이미지만 사용한다.
3. 3d view의 결과물은 실제 적용된 모습과 다를 수 있으니, 참고만 한다.
---


패킹 시에는 몇 초 정도, 로딩이 생길 수 있습니다.




그리고 가장 중요한 점은 패킹한 결과물이 투명하더라도, 해당 채널의 이미지 정보는 남아 있다는 것입니다.
참고로 해당 채널에 대한 정보는 포토샵에서는 보이지 않습니다.(png파일 사용 시)


하지만 게임 엔진에서 해당 이미지를 확인해보면 R, G, B, A 채널의 정보가 분리되어 온전하다는 것을 확인할 수 있습니다.



예시)

![image](https://github.com/user-attachments/assets/bf4bd372-1c10-4343-a367-97fcaec7cdf8)

해당 이미지에 알파값이 1인 경우는 모든 채널이 잘 섞여 보인 듯 하지만,

![image](https://github.com/user-attachments/assets/54222f17-52a7-4ab6-8844-f48dd5ec8817)

알파값을 0으로 Invert해버리면 결과물이 투명해 보이지 않습니다.

하지만, 해당 이미지를 패킹해서 유니티로 가져간다면

![image](https://github.com/user-attachments/assets/b070ce56-d8c3-432d-823a-1c63216f05f6)

![image](https://github.com/user-attachments/assets/71bac4f1-44d6-4696-8160-cbd190841352)

![image](https://github.com/user-attachments/assets/ed55e3aa-9ff9-4539-b98c-def47cc5b3ea)

![image](https://github.com/user-attachments/assets/dd4d1788-a963-4907-b629-b8e76e6026af)

모든 채널의 이미지가 살아있는 것을 볼 수 있습니다


![image](https://github.com/user-attachments/assets/b42af2e9-08f1-47a2-8fcf-9e5142ab138c)


해당 텍스쳐의 Alpha is Transperency 설정은 절대 켜선 안 됩니다.
만약에 해당 설정은 킨다면


![image](https://github.com/user-attachments/assets/5d19a6ff-1538-4b90-97bd-5d999e1bb38a)


이처럼 모든 정보가 투명하게 보이게 됩니다.
