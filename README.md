# FLOW
Kotlin DSL for Minecraft Bukkit API

### Orientation  
  * #### 가독성  
  * #### 중복코드 제거  
  * #### 날먹  
  * #### 간결화  
  * #### 선언적 프로그래밍  
  * #### 디버깅 + 유지보수  

* ### Features

 * #### InVENC
   -   인벤토리 UI 구성 + 액션 정의   
 * #### ItemX
   -   커스텀 아이템 + 액션 정의

 * ### DoLL
   -   네임스페이스 기반 NPC 엔티티 생성

 * ### Particle
   -   png 기반 파티클 생성 제어  

* ### FireWork
  -   png 기반 폭죽 발사 제어

* ### Moremmand
  -   커맨드 명령어 DSL

* ### Event
  -   이벤트 블록
  -   자동 인자 파싱

* ### Log
  * 로그 자동 로딩

* ### CfgLoader
  -   yml 파일 제어

* ### Protocol
  -   패킷 제어 가이드

* ### ApIListener
  *  전용 클라이언트를 이용한 

* ### CoinKid
  -   실버, 골드, 다이아 기반 재화 관리
      

마인크래프트 서버에는 대부분 플러그인이라는 외부 파일이 들어갑니다.  
플러그인은 보통 java나 kotlin을 사용해 버킷 api의 프레임워크에 기반을 두고 개발합니다.  
아래는 버킷 api로 간단한 UI창을 구현한 코드입니다.
``` kotlin
    // GPT로 뽑은 예시입니다.
    @EventHandler
    fun onInventoryClick(event: InventoryClickEvent) {
        if (event.view.title == "My Custom Inventory") {
            event.isCancelled = true
            event.currentItem?.let {
                if (it.type != Material.AIR) {
                    event.whoClicked.sendMessage("You clicked on: ${it.type}")
                }
            }
        }
    }

    fun openCustomInventory(player: org.bukkit.entity.Player) {
        val inv: Inventory = Bukkit.createInventory(null, 9, "My Custom Inventory")
        inv.setItem(0, ItemStack(Material.DIAMOND)) // 다이아몬드 추가
        player.openInventory(inv)
    }
    
                                        
```
버킷 API는 객체지향 원리에 따라 설계되었지만,  
아무래도 복잡한 기능을 커스터마이징하려다보면 위와 같이 코드가 매우 길어지고 드러워집니다.  

그것을 완화하려고 제아무리 깔끔하게 코드를 짜서 책임을 분리하니 뭐니 해도   
결국 개발자는 장황하고 커다란 문법들에 의해 크게 고통받게 됩니다.  
그래서 이런 귀찮은 구현과정을 단 한줄만으로 개날먹할수 있게 해주는 프레임워크가 필요해졌습니다.  
FLOW는 Kotlin DSL을 기반으로 개발되어 보다 선언적이고 날먹적인 개발을 지원합니다.  
아래는 FLOW의 InVENC로 아까의 기능을 구현한 코드입니다.  
``` kotlin
InVENC("", 9){ //인벤토리를 고유의 companion object map에 캐싱
  setItem(0,"", listOf("",""), 1, false){
    onClick {  } //클릭시 실행될 메서드 주입
    onScroll() {  } //스크롤 각도당 실행될 메서드 주입(별도의 조건문 필요)
  }
}     
```  

이렇게 기능에 따라 한줄, 많아도 세줄 안으로 구현이 가능한 코드가 완성되었습니다.  
별도의 openInv() 메서드로 인벤토리 이름을 찾아 열게 할 수 있습니다.  

* ## NOTE
  * FLOW에 사용된 DSL 타입 선언적 프로그래밍 기법은 각별님의 _kommand_ 에서 영감을 받았습니다.
  * 라이선스는 GPL-3.0이며 변경 혹은 삭제를 금합니다.

* ## Contributors
  * #### MoreGrayner
