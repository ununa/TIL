# content
```content``` 속성은 생성한 값으로 요소를 대체한다.

### Tooltip 만들기

#### HTML
```html
<span data-tooltip-text="tooltip"></span>
<span class="break-type" data-tooltip-text="">THIS IS LONG TOOLTIP</span>
```

#### CSS
```css
/*
	css-only-tooltip version 1.0.0
	ⓒ 2015 AHN JAE-HA http://github.com/eu81273
	MIT License
*/


[data-tooltip-text]:hover {
	position: relative;
}

[data-tooltip-text]:hover:after {
    border:1px solid #d9d9d9;
	background-color: #fff;
    background-color: rgba(255, 255, 255, 1);
    
	-webkit-box-shadow: 2px 2px 5px 0 rgba(0, 0, 0, 0.2);
	-moz-box-shadow: 2px 2px 5px 0 rgba(0, 0, 0, 0.2);
	box-shadow: 2px 2px 5px 0 rgba(0, 0, 0, 0.2);

	-webkit-border-radius: 3px;
	-moz-border-radius: 3px;
	border-radius: 3px;

	color: #333;
    font-size: 12px;
    font-weight: 500;
	content: attr(data-tooltip-text);

    margin-bottom: 10px;
	top: -9px;
	left: calc(100% + 5px);    
	padding: 7px 12px;
	position: absolute;
	width: auto;

    z-index: 9999;
    text-align:left;
    line-height:1.4;
    color:#333
}
.break-type[data-tooltip-text]:hover:after {
    content:"My Heart leaps up when I behold A rainbow in the sky: So was it when my life began; So be it now I am a man So be it when I shall grow old, Or let me die! The Child is father of the Man; And I could wish my days to be Bound each to by natural piety.";
    white-space:pre;
}
```

#### 참고링크:
https://developer.mozilla.org/ko/docs/Web/CSS/content