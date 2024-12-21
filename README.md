<!DOCTYPE html>
<html>
 <head>
  <meta charset="UTF-8">

  <title>圣诞树</title>

  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/normalize/5.0.0/normalize.min.css">

  <style>
   *
   {
    box-sizing: border-box;
   }


   body
   {
    margin: 0;
    height: 100vh;
    overflow: hidden;
    display: flex;
    align-items: center;
    justify-content: center;
    background: #161616;
    color: #c5a880;
    font-family: sans-serif;
   }


   label
   {
    display: inline-block;
    background-color: #161616;
    padding: 16px;
    border-radius: 0.3rem;
    cursor: pointer;
    margin-top: 1rem;
    width: 300px;
    border-radius: 10px;
    border: 1px solid #c5a880;
    text-align: center;
   }


   ul
   {
    list-style-type: none;
    padding: 0;
    margin: 0;
   }


   .btn
   {
    background-color: #161616;
    border-radius: 10px;
    color: #c5a880;
    border: 1px solid #c5a880;
    padding: 16px;
    width: 300px;
    margin-bottom: 16px;
    line-height: 1.5;
    cursor: pointer;
   }
   .separator
   {
    font-weight: bold;
    text-align: center;
    width: 300px;
    margin: 16px 0px;
    color: #a07676;
   }


   .title
   {
    color: #a07676;
    font-weight: bold;
    font-size: 1.25rem;
    margin-bottom: 16px;
   }


   .text-loading
   {
    font-size: 2rem;
   }
  </style>

  <script>
   window.console = window.console || function(t) {};
  </script>



  <script>
   if (document.location.search.match(/type=embed/gi)) {
    window.parent.postMessage("resize", "*");
   }
  </script>


 </head>

 <body translate="no" >
  <script src="https://cdn.jsdelivr.net/npm/three@0.115.0/build/three.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/three@0.115.0/examples/js/postprocessing/EffectComposer.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/three@0.115.0/examples/js/postprocessing/RenderPass.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/three@0.115.0/examples/js/postprocessing/ShaderPass.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/three@0.115.0/examples/js/shaders/CopyShader.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/three@0.115.0/examples/js/shaders/LuminosityHighPassShader.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/three@0.115.0/examples/js/postprocessing/UnrealBloomPass.js"></script>

  <div id="overlay">
   <ul>
    <li class="title">请选择音乐</li>
    <li>
     <button class="btn" id="btnA" type="button">
      Snowflakes Falling Down by Simon Panrucker
     </button>
    </li>
    <li><button class="btn" id="btnB" type="button">This Christmas by Dott</button></li>
    <li><button class="btn" id="btnC" type="button">No room at the inn by TRG Banks</button></li>
    <li><button class="btn" id="btnD" type="button">Jingle Bell Swing by Mark Smeby</button></li>
    <li class="separator">或者</li>
    <li>
     <input type="file" id="upload" hidden />
     <label for="upload">Upload File</label>
    </li>
   </ul>
  </div>

  <script id="rendered-js" >
   const { PI, sin, cos } = Math;
   const TAU = 2 * PI;

   const map = (value, sMin, sMax, dMin, dMax) => {
    return dMin + (value - sMin) / (sMax - sMin) *
