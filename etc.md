운영체제는 소프트웨어다.

HW 는 physical SW는 logical(virtual)이다.

운영체제는 app 서비스를 서포트하고 아래로는 관리 제어한다. 

현재는 멀티프로세서이기에 위로 잘 관리하고 이상한 프로그램을 잘 막고 관리해야 한다. 

인터럽트는 한 마디로 누가 띵똥 벨 누르는 것이라 생각하면 된다. 컴퓨터는 혼자 작동하지 않고 주변 기기가 붙어있기에 서로 통신, 입출력을 할 때 인터럽트가 발생한다. 

os가 다른 기기들을 제어한다. API application programming interface 중 printf를 통해 정보를 user단에서 kernel모드로 넘어갈 때 그 코드를 system call이라고 한다. 

모든 입출력은 읽든지 쓰던지. 

2023.03.09(목) w2b ch4&6

아버지가 컴퓨터 하나만 주시고 형제가 나눠쓰면 좋아? 싫지!
1) 쓰는 시간 2) 용량을 다 써버리면, 데이터를 지워버리면? 3) 사생활

- OS에서 어떤 기능을 먼저 작동?
PROCESS general vs specific

general : sequence of work, running instance of a program
os덕분에 seperating computer with program 또 여러개를 차례대로 할 수 있다. 
오에스가 없으면 테트리스만 되는 컴퓨터를 떠올리면 된다. in sequence

time sharing 
팀모임을 하게 하는 것 : 메카니즘 
그걸 하게 하는 문화나 요소들 : policy

(low)mechanism : 문제를 인식하기 위한 것
(high)policy 는 strategy.
context = program counter(mouse cursor)

context switch가 good experience를 제공하는 것은 아니다. 

who design the context ? policy.
concern을 나눈다. 컴퓨팅은 항상 devide and conquer. 

하나의 솔루션의 두가지 측면 mechanism and process

concurrency vs parallelism
concurrency degree of processing same time(유튜브하면서 숙제하고 밥도 먹고..)
parallelism degree of capability(실제로는 하나를 하지만 스위치를 하는 것) 만약 일을 분할할 수 없을 수도 있기에 p가 c를 보장하는 것은 아니다. 
utilize parallelism maximize concurrency

concurrency : logical
parallelism : space

context : snapshot 지금 진행되는 프로세스
memory state : PC, 

CPU states
I/O 이미 OS에게 통제

OS는 operation 
process creating : initiating
loading
loading  data : allocate kernel object or new process name it empty place 에 배치
파일로 disk에서 가져와야 그래서 OS가 file을 

eager loading : 한번에 다! 비용
lazy : 요구대로만


### process Creation
pid라고 불린다. process가 child process를 만든다. 인간처럼
첫번째 친구가 바로 system d, init d라고 한다 kernel이 만든
그런데 왜?
처음에 프로세스는 delegate a task를 하기 위해 
function은 다른 function이 불러줘야call한다. 
마찬가지이다. 그래서 caller callee가 존재
프로세스가 많을 때 통제를 해야 하는데 누가 그 능력을? 
그래서 하나의 프로세스, 부모 프로세스가 자녀 프로세스를 관리하는 게 좋다고 생각했다. 
그래서 프로세스는 Tree형태이다. 

pastree를 보면 트리를 볼 수 있다. 

spawn은 만들고 관리하는 것
자녀와 부모 프로세스는 resource를 나눠쓸 수 있다. 

UNIX fork()라는 하위가지를 만드는 그런 게 있다고..

idle = ready












Process vs thread
















