# jQuery를 이용한 Sticky.
- 모든건 나의 감으로 한 코딩이라 당연 오류날 수 있음.

### Sticky-01
#### (조건)
- 반응형이 아닌 고정된 너비 값이 있을 것
- 현재 창이 max-width보다 작을 때 생기는 가로스크롤 대응.
- top 고정 후 stopper에 도착하면 bottom sticky로 변환.
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Sample</title>
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300&display=swap" rel="stylesheet">
<style>
body {
    background: #fff;
    color: #666;
    font: 14px/1.6em 'Noto Sans KR', sans-serif;;
    text-align: left;
}
.container {
    width: 1000px;
    margin: 0 auto;
    padding: 0 10px;
}
header {
    position: relative;
    width: 100%;
    height: 100px;
    background-color: #ccc
}
nav {
    width: 100%;
    margin-bottom: 10px;
    background-color: :#999;
    color: #fff
}
main {
    position: relative;
}
main:after {
    content: '';
    clear: both;
    display: block
}
aside {
    float: left;
    width: 320px;
    background-color: #f4f4f4;
    box-sizing: border-box;
    padding: 10px;
}
aside.is-absolute {
    position: absolute
}
aside.is-fixed {
    position: fixed
}
.content {
    float: right;
    width: 640px;
}
footer {
    width: 100%;
    height: 300px;
    margin-top: 10px;
    background-color: #999;
}
</style>
</head>
<body>

<div class="container">
    <header>HEADER</header>
    <nav>NAV</nav>
    <main class="js-sticky-wrapper">
        <aside class="js-sticky">
            <h2>제목 1</h2>
            <p>까닭이요, 나는 릴케 위에 아름다운 새워 이름과, 애기 거외다. 무덤 벌써 않은 헤일 봅니다. 불러 마디씩 그러나 소녀들의 이름과, 까닭이요, 다 버리었습니다. 별이 별 별을 겨울이 별 까닭입니다. 소녀들의 내 흙으로 마리아 계십니다. 이네들은 하나 시와 옥 없이 다하지 까닭입니다. 벌레는 나의 불러 소녀들의 못 이름과, 아이들의 오는 아침이 있습니다. 오면 헤일 이 오는 지나고 이름과, 별 헤는 된 계십니다. 않은 말 가을 있습니다. 가득 내일 무엇인지 보고, 노루, 별 우는 거외다. 벌레는 까닭이요, 소녀들의 가슴속에 별 없이 어머니, 까닭이요, 나는 까닭입니다.</p>
            <h2>제목 2</h2>
            <p>까닭이요, 나는 릴케 위에 아름다운 새워 이름과, 애기 거외다. 무덤 벌써 않은 헤일 봅니다. 불러 마디씩 그러나 소녀들의 이름과, 까닭이요, 다 버리었습니다. 별이 별 별을 겨울이 별 까닭입니다. 소녀들의 내 흙으로 마리아 계십니다. 이네들은 하나 시와 옥 없이 다하지 까닭입니다. 벌레는 나의 불러 소녀들의 못 이름과, 아이들의 오는 아침이 있습니다. 오면 헤일 이 오는 지나고 이름과, 별 헤는 된 계십니다. 않은 말 가을 있습니다. 가득 내일 무엇인지 보고, 노루, 별 우는 거외다. 벌레는 까닭이요, 소녀들의 가슴속에 별 없이 어머니, 까닭이요, 나는 까닭입니다.</p>
        </aside>
        <div class="content">
            <h1>별 헤는 밤</h1>
            <p>까닭이요, 나는 릴케 위에 아름다운 새워 이름과, 애기 거외다. 무덤 벌써 않은 헤일 봅니다. 불러 마디씩 그러나 소녀들의 이름과, 까닭이요, 다 버리었습니다. 별이 별 별을 겨울이 별 까닭입니다. 소녀들의 내 흙으로 마리아 계십니다. 이네들은 하나 시와 옥 없이 다하지 까닭입니다. 벌레는 나의 불러 소녀들의 못 이름과, 아이들의 오는 아침이 있습니다. 오면 헤일 이 오는 지나고 이름과, 별 헤는 된 계십니다. 않은 말 가을 있습니다. 가득 내일 무엇인지 보고, 노루, 별 우는 거외다. 벌레는 까닭이요, 소녀들의 가슴속에 별 없이 어머니, 까닭이요, 나는 까닭입니다.</p>
            <p>별 별 이 거외다. 사랑과 묻힌 아스라히 언덕 이런 이제 있습니다. 소학교 하나 옥 그리워 가을로 보고, 봅니다. 내린 언덕 까닭이요, 계십니다. 덮어 풀이 북간도에 이름과, 그리고 밤을 이름과, 토끼, 딴은 봅니다. 강아지, 별 걱정도 시인의 봄이 내 벌써 새겨지는 봅니다. 불러 이름과, 말 계십니다. 둘 헤일 별 남은 하나에 한 어머니, 봅니다. 소녀들의 남은 많은 사람들의 위에 동경과 무성할 봅니다. 소학교 책상을 언덕 가을 쉬이 풀이 마리아 버리었습니다. 가난한 어머님, 시와 불러 소녀들의 흙으로 멀듯이, 까닭입니다.</p>
            <p>추억과 내 이네들은 그리워 비둘기, 하나에 지나가는 동경과 이름과, 거외다. 많은 마리아 이제 못 책상을 가득 나의 남은 계집애들의 까닭입니다. 하나 별 못 우는 별이 하늘에는 시인의 무덤 봅니다. 쉬이 하나에 어머니, 이름과, 남은 거외다. 가득 남은 별 말 별에도 비둘기, 듯합니다. 봄이 하나에 릴케 추억과 봅니다. 피어나듯이 이름과, 가을로 계집애들의 어머니, 까닭입니다. 하나에 계집애들의 계절이 아름다운 멀듯이, 있습니다. 된 시와 별 나의 까닭입니다. 가난한 내 시와 이웃 프랑시스 아스라히 별빛이 아름다운 계십니다.</p>
            <p>이런 이름을 덮어 패, 다 까닭입니다. 이름과, 내 별빛이 지나고 풀이 프랑시스 헤일 멀리 남은 버리었습니다. 오면 가슴속에 옥 걱정도 불러 벌레는 무성할 까닭입니다. 잔디가 소녀들의 이웃 그리고 나는 별이 이름자를 나의 멀리 까닭입니다. 묻힌 같이 이름과, 그러나 써 있습니다. 하나의 이국 말 무성할 프랑시스 이름자 패, 별 이 거외다. 써 이름자 피어나듯이 시와 경, 듯합니다. 나의 강아지, 별들을 된 사랑과 이름과 멀리 토끼, 나의 거외다. 멀리 이름과 나는 하나에 봅니다. 위에 그리고 지나가는 밤이 헤는 청춘이 거외다.</p>
            <p>별 불러 없이 멀듯이, 노루, 풀이 써 비둘기, 까닭입니다. 가을 언덕 아직 비둘기, 까닭이요, 있습니다. 벌레는 이름과, 별을 다하지 잔디가 그러나 별 있습니다. 이름과, 다 무성할 이름을 토끼, 나의 너무나 하나에 다하지 까닭입니다. 벌레는 이네들은 이름을 써 가득 멀듯이, 거외다. 잠, 풀이 하나 피어나듯이 가난한 까닭입니다. 내일 언덕 멀리 어머니, 불러 추억과 하늘에는 아직 있습니다. 애기 이름과, 가난한 차 사랑과 때 하나에 다하지 계십니다. 까닭이요, 가득 어머니, 가슴속에 릴케 까닭입니다. 오면 시인의 새겨지는 벌써 하나 걱정도 소녀들의 않은 거외다. 위에 묻힌 옥 내 추억과 프랑시스 피어나듯이 까닭입니다.</p>
            <p>둘 계집애들의 가득 별 하나에 때 있습니다. 별 비둘기, 하나에 이름과, 이름자 아침이 나의 봅니다. 아름다운 별 책상을 했던 잠, 이런 무성할 봅니다. 겨울이 묻힌 보고, 위에 별 아직 가슴속에 버리었습니다. 이름과, 피어나듯이 하나에 이네들은 가을 버리었습니다. 이웃 이름자 벌써 별 이네들은 그러나 그리고 아직 봅니다. 많은 책상을 이름과, 거외다. 릴케 언덕 하나에 자랑처럼 어머님, 하나에 듯합니다. 밤을 밤이 불러 불러 다 버리었습니다.</p>
            <p>아무 어머니, 멀리 까닭입니다. 어머니, 새워 부끄러운 내린 청춘이 밤을 불러 이런 아직 계십니다. 이름과 비둘기, 별빛이 별 벌써 둘 그리워 하나에 동경과 봅니다. 이름자 그리워 아이들의 이제 무엇인지 아스라히 별 있습니다. 쉬이 내일 어머님, 이름을 듯합니다. 많은 애기 불러 책상을 언덕 나의 내일 무엇인지 있습니다. 않은 밤을 무성할 릴케 내 시와 걱정도 어머님, 듯합니다. 별 속의 당신은 말 부끄러운 나는 봅니다. 경, 청춘이 내일 피어나듯이 아스라히 딴은 옥 봅니다.</p>
            <p>하나의 어머님, 책상을 별 피어나듯이 새겨지는 계십니다. 쓸쓸함과 같이 별 노새, 어머니, 버리었습니다. 지나가는 다 계절이 헤는 버리었습니다. 어머니, 하나의 강아지, 어머님, 가득 이름과 버리었습니다. 위에 시인의 때 너무나 위에도 것은 새겨지는 버리었습니다. 노새, 멀리 노루, 흙으로 쉬이 봅니다. 말 헤일 멀리 그리워 까닭입니다. 가득 까닭이요, 위에도 묻힌 버리었습니다. 당신은 풀이 잔디가 피어나듯이 하나에 것은 했던 별 하나에 봅니다.</p>
            <p>밤이 가을로 소녀들의 아이들의 파란 별 겨울이 계십니다. 멀리 경, 무덤 가난한 다하지 사람들의 까닭입니다. 라이너 많은 책상을 별 이네들은 토끼, 있습니다. 까닭이요, 시인의 우는 딴은 봅니다. 쓸쓸함과 무덤 애기 까닭입니다. 그러나 아직 했던 사랑과 북간도에 슬퍼하는 위에 계십니다. 별 까닭이요, 소녀들의 헤는 아스라히 라이너 가득 버리었습니다. 많은 쓸쓸함과 패, 너무나 거외다. 별이 추억과 이런 별에도 이름자 이네들은 내린 된 겨울이 버리었습니다. 쉬이 써 둘 이름과, 봅니다.</p>
            <p>무덤 그리워 지나가는 하나에 된 거외다. 하나에 지나가는 별 애기 어머님, 까닭입니다. 내린 나의 추억과 말 피어나듯이 무성할 있습니다. 같이 어머님, 했던 것은 별 듯합니다. 나의 그리고 이름자를 어머님, 시와 써 강아지, 듯합니다. 강아지, 다 이름과, 불러 이국 한 계집애들의 버리었습니다. 나는 이름을 별빛이 멀리 지나가는 없이 언덕 속의 옥 봅니다. 내린 하나 잠, 별 무성할 멀듯이, 못 까닭입니다. 된 계절이 이름자 듯합니다. 계절이 피어나듯이 내린 봅니다. 너무나 벌레는 멀리 내린 토끼, 쉬이 버리었습니다.</p>
        </div>
    </main>
    <footer class="js-sticky-stopper"></footer>
</div>

<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
<script>
$(document).ready(function() {

  var $sticky = $('.js-sticky');
  var $stickyrStopper = $('.js-sticky-stopper');
  var $stickyWrapper = $('.js-sticky-wrapper');
  var _minWidth = 1000;

  if (!!$sticky.offset()) { // make sure ".sticky" element exists

    var generalSidebarHeight = $sticky.outerHeight();
    var stickyWidth = $sticky.width();
    var stickyTop = $sticky.offset().top;
    var stickyLeft = $sticky.offset().left;
    var stickOffset = 0;
    var stickyStopperPosition = $stickyrStopper.offset().top;
    var stopPoint = stickyStopperPosition - generalSidebarHeight - stickOffset;
    var diff = stopPoint + stickOffset;

    $(window).bind('scroll resize', onScroll);

    // scroll function
    function onScroll(_left){
        var windowTop = $(window).scrollTop(); // returns number
        var windowLeft = $(window).scrollLeft();
        var wrapperLeft = $stickyWrapper.offset().left;

        //--- bottom.
        if (stopPoint < windowTop) {
            $sticky.addClass('is-absolute').removeClass('is-fixed').css({top: diff - stickyTop, left: 0, 'margin-left': 0});
        
        //--- middle.
        } else if (stickyTop < windowTop + stickOffset) {
            $sticky.addClass('is-fixed').removeClass('is-absolute').css({top: stickOffset });
            var _left = ($(window).width() < _minWidth) ? _left = $sticky.css({'left':stickyLeft - windowLeft}) : $sticky.css({'left':wrapperLeft});
            //Scroll X.

        //--- top.
        } else {
            $sticky.removeClass('is-absolute, is-fixed').css({top: 'initial', left: 0, 'margin-left': 0});
        }
    }
  }
});
</script>
</body>
</html>

```
