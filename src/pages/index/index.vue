<template>
  <view>
    <view id="toolbar">
      <view class="button" id="load">Load</view>
      <view class="button" id="save">Save</view>
      <!-- <view class="button disabled">Undo</view>
      <view class="button disabled">Redo</view>-->
      <view class="button" id="about">About</view>
    </view>
    <!-- 侧边栏 -->
    <view id="sidebar"></view>
    <!-- 工作区域 -->
    <view id="editor">
      <view class="contents">
        <view id="placeholder"></view>
        <canvas id="canvas2d"></canvas>
        <view id="nubs"></view>
      </view>
    </view>
    <view id="fade"></view>
    <view id="dialog"></view>
    <!-- <view id="loading">
      <script type="text/javascript">
  document.write("Loading...");
      </script>
      <noscript>Please enable JavaScript and refresh this page</noscript>
      <noscript>up the</noscript>
    </view>-->
  </view>
</template>

<script>
import "../../libs/glfx.js/glfx.js";
import "../../libs/jquery/jquery-1.5.1.min.js";
import "../../libs/jquery/jquery.ui.slider.js";
import obj from "../../js/script.js";
export default {
  data() {
    return {
      title: "Hello"
    };
  },
  mounted(){
	  obj();
  },
  onLoad() {},
  methods: {
	  
  }
};
</script>

<style>
/* * {
    cursor: default;
    -moz-user-select: none;
    -webkit-user-select: none;
} */

a {
  color: #fc0;
  cursor: pointer;
}
table {
  border-collapse: collapse;
}
td {
  padding: 0;
  vertical-align: top;
}
body {
  font: 12px Tahoma, sans-serif;
  text-shadow: 0 1px 0 black;
  background: #1b1917;
  color: white;
}

.ui-slider-handle {
  cursor: default;
  position: absolute;
  width: 12px;
  height: 12px;
  background: -moz-linear-gradient(#4b4947, #32302d);
  background: -webkit-gradient(
    linear,
    left top,
    left bottom,
    from(#4b4947),
    to(#32302d)
  );
  -moz-box-shadow: inset 0 1px 0 #5b5957, 0 -1px 0 black, 0 1px 0 black,
    -1px 0 0 black, 1px 0 0 black, 0 1px 1px #111;
  -webkit-box-shadow: inset 0 1px 0 #5b5957, 0 -1px 0 black, 0 1px 0 black,
    -1px 0 0 black, 1px 0 0 black, 0 1px 1px #111;
  margin: -6px;
  border-radius: 6px;
  -moz-border-radius: 7px;
  -webkit-border-radius: 7px;
}

.ui-state-active {
  background: -moz-linear-gradient(#6b6967, #42403d);
  background: -webkit-gradient(
    linear,
    left top,
    left bottom,
    from(#6b6967),
    to(#42403d)
  );
}

.ui-state-focus {
  outline: none;
}

.button {
  display: inline-block;
  padding: 1px 15px;
  border-radius: 4px;
  vertical-align: top;
  background: -moz-linear-gradient(#4b4947, #32302d);
  background: -webkit-gradient(
    linear,
    left top,
    left bottom,
    from(#4b4947),
    to(#32302d)
  );
  -moz-box-shadow: inset 0 1px 0 #5b5957, 0 -1px 0 black, 0 1px 0 black,
    -1px 0 0 black, 1px 0 0 black, 0 1px 1px #111;
  -webkit-box-shadow: inset 0 1px 0 #5b5957, 0 -1px 0 black, 0 1px 0 black,
    -1px 0 0 black, 1px 0 0 black, 0 1px 1px #111;
}

.button:active {
  padding: 2px 15px 0 15px;
  background: #272727;
  -moz-box-shadow: inset 0 0 10px #070707, inset 0 0 5px #070707,
    0 1px 0 #4b4947;
  -webkit-box-shadow: inset 0 0 10px #070707, inset 0 0 5px #070707,
    0 1px 0 #4b4947;
}

.button.disabled {
  color: #111;
  padding: 1px 15px;
  text-shadow: 0 1px 0 #4b4947;
  background: -moz-linear-gradient(#3b3937, #2b2927);
  background: -webkit-gradient(
    linear,
    left top,
    left bottom,
    from(#3b3937),
    to(#2b2927)
  );
  -moz-box-shadow: inset 0 1px 0 #4b4947, 0 -1px 0 #111, 0 1px 0 #111,
    -1px 0 0 #111, 1px 0 0 #111, 0 1px 1px #111;
  -webkit-box-shadow: inset 0 1px 0 #4b4947, 0 -1px 0 #111, 0 1px 0 #111,
    -1px 0 0 #111, 1px 0 0 #111, 0 1px 1px #111;
}

#toolbar {
  z-index: 2;
  background: -moz-linear-gradient(#3b3937, #2b2927);
  background: -webkit-gradient(
    linear,
    left top,
    left bottom,
    from(#3b3937),
    to(#2b2927)
  );
  -moz-box-shadow: 0 1px 0 black;
  -webkit-box-shadow: 0 1px 0 black;
  position: absolute;
  left: 0;
  top: 0;
  right: 0;
  height: 44px;
}

#toolbar .button {
  float: left;
  line-height: 27px;
  margin: 7px 0 0 7px;
}

#sidebar {
  z-index: 1;
  position: absolute;
  left: 0;
  top: 44px;
  bottom: 0;
  width: 300px;
  padding: 0 0 20px 0;
  background: #3b3937;
  overflow-x: hidden;
  overflow-y: auto;
  -moz-box-shadow: 1px 0 0 black;
  -webkit-box-shadow: 1px 0 0 black;
}

#sidebar .header {
  padding: 15px 0 5px 15px;
  color: #777;
}

#sidebar .item {
  position: relative;
  margin: 0 -10px;
  padding: 0 40px;
}

#sidebar .item .title {
  height: 25px;
  font-weight: bold;
  line-height: 25px;
}

#sidebar .item .contents {
  padding: 0 0 20px 0;
  display: none;
}

#sidebar .item .contents table {
  padding: 0 0 5px 0;
  color: #777;
  width: 100%;
}

#sidebar .item .contents td {
  width: 0;
  white-space: nowrap;
  padding-top: 5px;
}

#sidebar .item .contents td + td {
  width: 100%;
  padding-left: 15px;
}

#sidebar .item .contents .button {
  line-height: 24px;
  margin: 15px 0 0 0;
}

#sidebar .item .contents .reset {
  text-decoration: underline;
  display: inline-block;
  line-height: 24px;
  margin: 15px 0 0 15px;
  cursor: pointer;
  color: #777;
}

#sidebar .item .contents .slider {
  position: relative;
  margin: 8px 0 0 0;
  border-top: 1px solid #222;
  border-bottom: 1px solid #555;
}

#sidebar .item .contents .segmented {
  margin: -3px 0 0 0;
}

#sidebar .item .contents .segment {
  color: white;
  line-height: 20px;
  display: inline-block;
  padding: 1px 15px;
  vertical-align: top;
  background: -moz-linear-gradient(#4b4947, #32302d);
  background: -webkit-gradient(
    linear,
    left top,
    left bottom,
    from(#4b4947),
    to(#32302d)
  );
  -moz-box-shadow: inset 0 1px 0 #5b5957, 0 -1px 0 black, 0 1px 0 black,
    -1px 0 0 black, 1px 0 0 black, 0 1px 1px #111;
  -webkit-box-shadow: inset 0 1px 0 #5b5957, 0 -1px 0 black, 0 1px 0 black,
    -1px 0 0 black, 1px 0 0 black, 0 1px 1px #111;
}

#sidebar .item .contents .segment.selected {
  padding: 2px 15px 0 15px;
  background: #272727;
  -moz-box-shadow: inset 0 0 10px #070707, inset 0 0 5px #070707,
    0 1px 0 #4b4947;
  -webkit-box-shadow: inset 0 0 10px #070707, inset 0 0 5px #070707,
    0 1px 0 #4b4947;
}

#sidebar .item .contents .segment:first-child {
  -webkit-border-top-left-radius: 5px;
  -webkit-border-bottom-left-radius: 5px;
}

#sidebar .item .contents .segment:last-child {
  -webkit-border-top-right-radius: 5px;
  -webkit-border-bottom-right-radius: 5px;
}

#sidebar .item .contents .curves {
  width: 200px;
  height: 200px;
  margin: 10px 0;
  border: 1px solid #4b4947;
}

#sidebar .item.active {
  background: #272727;
  -moz-box-shadow: inset 0 0 6px #070707, inset 0 0 3px #070707, 0 1px 0 #4b4947;
  -webkit-box-shadow: inset 0 0 6px #070707, inset 0 0 3px #070707,
    0 1px 0 #4b4947;
}

#sidebar .item.active .title {
  line-height: 27px;
}

#sidebar .item.active .contents .slider {
  margin: 8px 0 0 0;
  border-top: 1px solid black;
  border-bottom: 1px solid #333;
}

#editor {
  position: absolute;
  left: 300px;
  top: 44px;
  right: 0;
  bottom: 0;
  overflow: auto;
  padding: 30px;
}

#editor .contents {
  position: relative;
  display: inline-block;
  -moz-box-shadow: 0 0 10px black, 0 0 5px black;
  -webkit-box-shadow: 0 0 10px black, 0 0 5px black;
  background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQAQMAAAAlPW0iAAAABlBMVEW/v7////+Zw/90AAAAEUlEQVQI12P4z8CAFWEX/Q8Afr8P8erzE9cAAAAASUVORK5CYII=);
}

#editor .contents canvas {
  vertical-align: top;
}

#editor .contents #canvas2d {
  position: absolute;
  left: 0;
  top: 0;
}

#editor .contents #nubs {
  position: absolute;
  left: 0;
  top: 0;
  overflow: hidden;
}

#editor .contents .nub {
  position: absolute;
  width: 12px;
  height: 12px;
  cursor: move;
  margin: -6px;
  background: -moz-linear-gradient(#4b4947, #32302d);
  background: -webkit-gradient(
    linear,
    left top,
    left bottom,
    from(#4b4947),
    to(#32302d)
  );
  -moz-box-shadow: inset 0 1px 0 #5b5957, 0 -1px 0 black, 0 1px 0 black,
    -1px 0 0 black, 1px 0 0 black, 0 1px 1px #111;
  -webkit-box-shadow: inset 0 1px 0 #5b5957, 0 -1px 0 black, 0 1px 0 black,
    -1px 0 0 black, 1px 0 0 black, 0 1px 1px #111;
  border-radius: 6px;
}

#fade {
  z-index: 3;
  display: none;
  position: absolute;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
}

#dialog {
  z-index: 4;
  display: none;
  position: absolute;
  left: 50%;
  top: 0;
  width: 650px;
  margin-left: -325px;
  padding: 20px;
  background: #32302d;
  border: 1px solid black;
  -moz-box-shadow: 0 0 50px black, 0 0 20px rgba(0, 0, 0, 0.5);
  -webkit-box-shadow: 0 0 50px black, 0 0 20px rgba(0, 0, 0, 0.5);
}

#dialog .contents {
  padding-bottom: 20px;
  line-height: 16px;
}

#dialog .contents .images {
  padding: 15px 0 8px 0;
}

#dialog .contents .credits,
#dialog .contents .credits a {
  font-style: italic;
  font-size: 10px;
  color: #777;
}

#dialog .contents img {
  margin: 0 7px 7px 0;
  border: 1px solid black;
  -moz-box-shadow: 0 1px 2px rgba(0, 0, 0, 0.5);
  -webkit-box-shadow: 0 1px 2px rgba(0, 0, 0, 0.5);
}

#dialog .button {
  position: relative;
  line-height: 24px;
  margin-right: 7px;
}

#dialog input.upload {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  opacity: 0;
}

#loading {
  text-align: center;
  padding-top: 100px;
  position: absolute;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  z-index: 5;
  background: #2b2927;
  line-height: 16px;
}

#loading .sadface {
  font-size: 100px;
  line-height: 100px;
  padding-bottom: 40px;
}
</style>
