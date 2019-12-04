### 코드스쿼드 마스터즈 2020 온라인 과제 1단계 구현내용 (리팩토링 이후)

![step1_skeleton](/Users/jypsnewmac/Documents/GitHub/codesquad-jinhyung/step1_skeleton.jpeg)

* main 함수의 동작
  * main 함수를 실행시켜 전체 사항을 관리합니다.
  * baseball.message 출력하여 타자의 타석 입장을 알립니다.
  * 아웃 횟수가 아웃 제한과 같기 전까지 while문으로 아래의 사항을 반복 실행합니다.
    * 새로운 타자마다 랜덤함수를 만듭니다.
    * 랜덤함수를 인자값으로 하여 `baseball.gamePlay()`에 넘겨주고 이를 실행합니다.
  * 아웃 횟수가 아웃 제한과 같으면 다음을 실행합니다.
    * 최종 안타 수를 저장된 안타 수에 따라 출력합니다.
    * 게임을 종료하고 이를 사용자에게 출력합니다.
* baseball 객체
  * baseball 객체는 게임에 필요한 프로퍼티 및 메소드를 담고 있습니다.
  * 타구마다 나올 수 있는 경우의 수를 담고 있으며, 이 외에도 스트라이크/볼/아웃 제한을 지정합니다.
  * baseball.player 객체
    * 현재 타자의 횟수(몇 번째 타자인지)를 저장합니다.
    * 현재 타자의 볼 횟수, 스트라이크 횟수, 안타 횟수를 저장합니다.
    * 볼 횟수와 스트라이크 횟수는 새로운 타자가 등장하면 0으로 초기화되는 프로퍼티입니다.
    * 전체 게임의 아웃 횟수를 저장합니다.
  * baseball.newPlayer 메소드
    * 새로운 타자를 등장하도록 만드는 메소드입니다.
    * 아웃 횟수가 3을 넘지 않았으면 다음을 실행합니다.
      * 타자의 횟수를 1 증가합니다.
      * baseball.message 메소드를 리턴합니다.
  * baseball.message 메소드
    * 새로운 타자가 타석에 등장했음을 알립니다. 현재 타자의 횟수를 가져옵니다.
  * baseball.checkBall/Strike/Out/Hit 메소드
    * 랜덤함수를 받아서 타구의 결과가 볼/스트라이크/아웃/안타인지 판단합니다.
    * 결과에 따라 필요한 횟수를 1 증가합니다.
    * 아웃과 안타는 baseball.print를 호출합니다.
    * 위의 사항을 모두 진행한 경우 TRUE를 리턴합니다. 아니면 FALSE를 리턴합니다.
  * baseball.determine 메소드
    * 타자의 볼 횟수가 볼 제한과 같거나 스트라이크 횟수가 스트라이크 제한과 같을 때, 해당 결과를 게임 진행상태에 반영하기 위한 역할을 수행합니다.
    * 타자의 볼 횟수가 볼 제한과 같으면 다음을 수행합니다.
      * 안타 횟수를 1 증가합니다.
      * 볼 횟수를 0으로 초기화합니다.
      * 4볼이므로 1안타임을 출력합니다.
      * TRUE를 리턴합니다.
    * 타자의 스트라이크 횟수가 스트라이크 제한과 같으면 다음을 수행합니다.
      * 아웃 횟수를 1 증가합니다.
      * 3스트라이크이므로 1아웃임을 출력합니다.
      * 스트라이크 횟수를 0으로 초기화합니다.
      * TRUE를 리턴합니다.
    * 위의 경우에 모두 맞지 않을 경우 FALSE를 리턴합니다.
  * baseball.playGame 메소드
    * 실제 타구를 진행하고, 상기한 메소드를 관리하는 역할을 합니다.
    * baseball.checkBall/Strike가 참이면 다음을 수행합니다.
      * baseball.determine 메소드가 참이면 다음을 수행합니다.
        * baseball.print 호출해서 출력함
        * baseball.newPlayer 리턴해서 새 타자를 호출함
      * baseball.determine 메소드가 참이 아닐 경우 다음을 수행합니다.
        * 새 타자를 호출하지 않고 baseball.print 호출해서 출력함
    * baseball.checkOut/Hit 메소드가 참이면 다음을 수행합니다.
      * 볼 횟수를 0으로 초기화합니다.
      * 스트라이크 횟수를 0으로 초기화합니다.
      * baseball.newPlayer를 리턴해서 새 타자를 호출합니다.
