# Lab13_test02

엑티비티 라이프 싸이클

onCreate -> onStart -> onResume => 화면 출력, 활성상태 - 화면에 보이고 있고 User Event(o)

onPause : Pause상태 - 화면 출력, User Event(x)
onStop : 비활성 상태 - 화면 X 화면에 보이지 않는 상태
onDestroy : 메모리 해제 

![image](https://github.com/pointmina/Lab13_test02/assets/68779817/3a81b881-71c8-4509-89ae-06aa8d80103e)

- 활성 : 액티비티 화면이 출력되고 있고 사용자가 이벤트를 발생시킬 수 있는 상태
- 일시정지 : 액티비티의 화면이 출력되고 있지만 사용자가 이벤트를 발생시킬 수 없는 상태
- 비활성 : 액티비티의 화면이 출력되고 있지 않은 상태

ex) 액티비티가 크리에이트 되어 있는 ㄱ상태에서 화면 회전을 하면 디스트로이드가 되고 다시 크리에이트가 되는데
이때 화면 회전 전에 상태 데이터를 저장해놨다가 다시 크리에이트 될때 복원한다.

활성 상태에서 비활성 상태가 되면 onPause() — onStop() 함수까지 호출됩니다. 
그리고 다시 액티비티를 화면에 보이면 onRestart() — onStart() — onResumeO 함수까지 호출되어 활성 상태가 됩니다
