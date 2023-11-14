# Lab13_test02 ~ 끝까지

#Lab12_test02
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

13-5 액티비티 ANR 문제와 코루틴

ANR(Activity Not Respond) : 오류상황 - 화면 반응 x -> 5초

시간이 오래 걸리는 업무가 있어서 막 돌아가고 있는데 유저가 그 중간에 이벤트를 발생시키면 오류가 날 가능성이 있따. 대표적인거 -> 네트워킹

해결? 
1. Thread --------- Main Thread : 엑티비티를 실행시키기 위해 시스템에서 발생시킨 수행흐름
2. Coroutine ------

![image](https://github.com/pointmina/Lab13/assets/68779817/9a73f4fd-6ad4-4383-97f5-793828524f68)

-> 이러면 ANR은 처리되지만 화면 출력에서 문제가 생긴다

why?
화면을 보여주는 View에는 Main Thread만 접근 가능하고 그 외의 개발자 쓰레드나 코루틴으로 접근하면 오류가 발생한다. So, Main Thread에 전달해서 뷰에 접근해야한다. 

코루틴
- 스코프가 있어야한다.
- 스코프는 성격이 같은 코루틴을 묶는 개념
- 한 스코프에서 여러 코루틴을 구동할 수 있으면 한 어플에 여러 스코프를 만들 수 있따.


val channel = Channel<Int>()
val backgroundscope = CoroutineScope(Dispatchers.Default + Job())
backgroundscope.launch {                ㄴ> 백그라운드에서 동작(시간이 오래 걸리는 작업)
  var sum = 0L
  var time = measureTimeMillis {
    for (i in 1..2_000_000_000) {
      sum += i
    }
  }
  Log.d("kkang", "time : $time")
  channel.send(sum.tolnt())
}
val mainScope = GlobalScope.launch Dispatchers.Main) {
  channel.consumeEach {               ㄴ> 메인 스레드에서 동작(화면에 결괏값 표지)
    binding.resultview.text = "sum : $it"
  }
}

![image](https://github.com/pointmina/Lab13/assets/68779817/ee097b81-71b8-4476-891c-0df82100d19e)

디스패처 : 스코프에서 구동한 코루틴이 어디에서 동작해야 하는지를 나타낸다.

















