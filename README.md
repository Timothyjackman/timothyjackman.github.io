<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>AE MODULAR PATCH INSPIRATION</title>
  <style>
    @font-face {
     font-family: Cocomat;
     src: url(cocomat-pro-bold.ttf);
    }
    body {background-color: #c4bfb5;}
    p   {font-family: Cocomat;}
    h1   {font-family: Cocomat;}
    h2   {font-family: Cocomat;}
    button {font-family: Cocomat;}
    input {font-family: Cocomat;}
    label {
      font-family: Cocomat;
    }
    .button {
      /* Green */
      border: none;
      color: white;
      padding: 8px 16px;
      text-align: center;
      text-decoration: none;
      display: inline-block;
      font-size: 16px;
      margin: 4px 2px;
      transition-duration: 0.4s;
      cursor: pointer;
    }
    .button5 {
      
      color: black;
      border: 2px solid #555555;
    }

    .button5:hover {
      background-color: #555555;
      color: white;
    }
  </style>
</head>
<body>


<script>
  var temp = ""
  var modules = []
  var module1 = ""
  var module2 = ""
  var module1id = 0
  var module2id = 0
  var i = 0
  const allmodules = ["2ATTCV","2CVADD-HQ","2CVTOOL","2ENV","2LFO","2OSC/d","2SIGNALAMP","2TONE","2VCA","3VCSWITCH","4ATTMIX","4ATTMIX FADER","4BUFFER","4VCA","6MUTE","ADSR","ALGODRONE","BEAT DIVIDER","CIRRUS","CVADDER-HQ","CVSHIFTER","DELAY (LOFI)","DIODEFILTER","DRONE38","DRONX","DRUMKIT 010","FILTER (WASP TYPE)","FMOS","GRAINS","Wonkystuff&apos;s BioT","JOYSTICK","KICK","Kurt&apos;s Dead Band","Kurt&apos;s Quad Boost","Kurt&apos;s The Great Divide","Kurt&apos;s Five steps","Kyaa&apos;s Euclid Grid","LOGIC","LOPAG (VACTROL LOPASS GATE)","MIXCONSOLE","MIXER 4-4","MM-DIV","MODULATORS","MS20 FILTER","MULTIFX","NOISE","NYLE FILTER","OR 2x4","ORNAMENT & CRIME","PHASER","POLAMIX","QUANTIZER","SAMPLE & HOLD","SAWVOX","SEQ16","SEQ8","SLEW / EDGE","SOLINA","SPRINGREVERB","SVFILTER","SWITCHMATRIX 4x4","TBD","TOPOGRAF","TRIP","TRIQ164","VCO","WAVEFOLDER","WAVETABLES","Wonkystuff&apos;s core1.ae","Wonkystuff&apos;s mm33","Wonkystuff&apos;s Moco","Wonkystuff&apos;s QVCA","Wonkystuff&apos;s RBSS","XMIX"]
  const cvin = [1,1,1,1,1,1,1,0,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,0,1,1,1,1,1,1,1,1,1,0,1,1,1,1,1,1,0,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,0,1,1,1,1,1,1,1,0,1,1,1,1,1,1,0]
  const audioin = [1,0,1,0,0,0,1,1,1,1,1,1,1,1,1,0,0,0,1,0,0,1,1,0,1,1,1,0,1,1,0,0,1,1,0,0,0,0,1,1,1,0,0,1,1,0,1,0,1,1,1,0,1,0,0,0,0,0,1,1,1,1,0,0,0,0,1,0,1,1,0,1,0,1]
  const cvout = [1,1,1,1,1,1,1,0,1,1,1,1,1,1,1,1,1,1,0,1,1,0,0,1,0,0,0,0,1,1,1,0,1,0,1,1,1,1,1,0,0,1,1,0,0,1,0,1,1,0,1,1,1,0,1,1,1,0,0,0,1,1,1,1,1,0,0,0,1,0,1,1,1,0]
  const audioout = [1,0,1,0,1,1,1,1,1,1,1,1,1,1,1,0,1,0,1,0,0,1,1,1,1,1,1,1,1,1,0,1,1,1,0,0,0,0,1,1,1,0,0,1,1,1,1,0,0,1,0,0,0,1,0,0,0,1,1,1,1,1,0,0,0,1,1,1,1,1,0,1,0,1]
  var done = false
  var avoid = -1
  function checkName(name) {
    return name == name;
  }
  function addModule(p1, p2) {
  	if (p2) {
    	modules.push(p1)
    } else {
    	modules.splice(modules.indexOf(p1),1)
    }
  	temp = "2CVTOOL"
    
  }
  function download() {
    var element = document.createElement('a');
    element.setAttribute('href', 'data:text/plain;charset=utf-8,' + encodeURIComponent(modules));
    element.setAttribute('download', "modules");

    element.style.display = 'none';
    document.body.appendChild(element);

    element.click();

    document.body.removeChild(element);
  }
  function loadFileAsText(){
    var fileToLoad = document.getElementById("fileToLoad").files[0];

    var fileReader = new FileReader();
    fileReader.onload = function(fileLoadedEvent){
        var readText = fileLoadedEvent.target.result;
        modules = readText.split(",")
        for (var i in modules) {
          
          document.getElementById(modules[i]).checked = true;
        }
    };

    fileReader.readAsText(fileToLoad, "UTF-8");
  }
  function generateInstruction() {
    done = false
    i=0
    while (done==false) {
      module1 = modules[Math.floor(Math.random()*modules.length)]
      module2 = modules[Math.floor(Math.random()*modules.length)]
      module1id = allmodules.findIndex(themodule => themodule === module1)
      module2id = allmodules.findIndex(themodule => themodule === module2)
      if (module1==module2) {
        //do nothing
        done = false
      } else if (cvout[module1id]+cvin[module2id]==2 || audioout[module1id]+audioin[module2id]==2) {
        done = true
        var tag = document.createElement("p");
        var text = document.createTextNode("PATCH ".concat(module1," TO ", module2));
        tag.appendChild(text);
        var element = document.getElementById("instructions");
        element.appendChild(tag);
      } 
      if (i==20) {
        done = true
      }
      i=i+1
    }
    
    
  }
  function deleteAll() {
    var element = document.getElementById("patches");
    element.innerHTML = ''
    var element = document.getElementById("instructions");
    element.innerHTML = ''
  }
  function generatePatch() {
    done = false
    i=0
    while (done==false) {
      module1 = modules[Math.floor(Math.random()*modules.length)]
      module2 = modules[Math.floor(Math.random()*modules.length)]
      module1id = allmodules.findIndex(themodule => themodule === module1)
      module2id = allmodules.findIndex(themodule => themodule === module2)
      if (module1==module2) {
        //do nothing
        done = false
      } else if (cvout[module1id]+cvin[module2id]==2 || audioout[module1id]+audioin[module2id]==2) {
        done = true
        var element = document.getElementById("patches");
        element.innerHTML = ''
        var tag = document.createElement("p");
        var text = document.createTextNode("BASE YOUR PATCH AROUND ".concat(module1));
        tag.appendChild(text);
        var element = document.getElementById("patches");
        element.appendChild(tag);
        var tag = document.createElement("p");
        var text = document.createTextNode("BUT DO NOT USE ".concat(module2));
        tag.appendChild(text);
        var element = document.getElementById("patches");
        element.appendChild(tag);
      } 
      if (i==20) {
        done = true
      }
      i=i+1
    }
    
    
  }
  function helppopupshow() {
    var element = document.getElementById("helppopup");
    element.style.display = "block"
  }
  function helppopuphide() {
    var element = document.getElementById("helppopup");
    element.style.display = "none"
  }
</script>
<div style="height:95vh;width:150pt;overflow:auto;position: absolute;overflow-x:hidden;">
  <button onclick="download()">download</button>
  <br>
  <input type="file" id="fileToLoad" onclick="loadFileAsText()"></td>
  <br>
  <button onclick="loadFileAsText()">load selected file</button><td>

  <br>
  
  <input type="checkbox" id="2ATTCV" onclick="addModule('2ATTCV',checked)"/><label for="checkbox">2ATTCV</label>
  <br>
  <input type="checkbox" id="2CVADD-HQ" onclick="addModule('2CVADD-HQ',checked)"/><label for="checkbox">2CVADD-HQ</label>
  <br>
  <input type="checkbox" id="2CVTOOL" onclick="addModule('2CVTOOL',checked)"/><label for="checkbox">2CVTOOL</label>
  <br>
  <input type="checkbox" id="2ENV" onclick="addModule('2ENV',checked)"/><label for="checkbox">2ENV</label>
  <br>
  <input type="checkbox" id="2LFO" onclick="addModule('2LFO',checked)"/><label for="checkbox">2LFO</label>
  <br>
  <input type="checkbox" id="2OSC/d" onclick="addModule('2OSC/d',checked)"/><label for="checkbox">2OSC/d</label>
  <br>
  <input type="checkbox" id="2SIGNALAMP" onclick="addModule('2SIGNALAMP',checked)"/><label for="checkbox">2SIGNALAMP</label>
  <br>
  <input type="checkbox" id="2TONE" onclick="addModule('2TONE',checked)"/><label for="checkbox">2TONE</label>
  <br>
  <input type="checkbox" id="2VCA" onclick="addModule('2VCA',checked)"/><label for="checkbox">2VCA</label>
  <br>
  <input type="checkbox" id="3VCSWITCH" onclick="addModule('3VCSWITCH',checked)"/><label for="checkbox">3VCSWITCH</label>
  <br>
  <input type="checkbox" id="4ATTMIX" onclick="addModule('4ATTMIX',checked)"/><label for="checkbox">4ATTMIX</label>
  <br>
  <input type="checkbox" id="4ATTMIX FADER" onclick="addModule('4ATTMIX FADER',checked)"/><label for="checkbox">4ATTMIX FADER</label>
  <br>
  <input type="checkbox" id="4BUFFER" onclick="addModule('4BUFFER',checked)"/><label for="checkbox">4BUFFER</label>
  <br>
  <input type="checkbox" id="4VCA" onclick="addModule('4VCA',checked)"/><label for="checkbox">4VCA</label>
  <br>
  <input type="checkbox" id="6MUTE" onclick="addModule('6MUTE',checked)"/><label for="checkbox">6MUTE</label>
  <br>
  <input type="checkbox" id="ADSR" onclick="addModule('ADSR',checked)"/><label for="checkbox">ADSR</label>
  <br>
  <input type="checkbox" id="ALGODRONE" onclick="addModule('ALGODRONE',checked)"/><label for="checkbox">ALGODRONE</label>
  <br>
  <input type="checkbox" id="BEAT DIVIDER" onclick="addModule('BEAT DIVIDER',checked)"/><label for="checkbox">BEAT DIVIDER</label>
  <br>
  <input type="checkbox" id="CIRRUS" onclick="addModule('CIRRUS',checked)"/><label for="checkbox">CIRRUS</label>
  <br>
  <input type="checkbox" id="CVADDER-HQ" onclick="addModule('CVADDER-HQ',checked)"/><label for="checkbox">CVADDER-HQ</label>
  <br>
  <input type="checkbox" id="CVSHIFTER" onclick="addModule('CVSHIFTER',checked)"/><label for="checkbox">CVSHIFTER</label>
  <br>
  <input type="checkbox" id="DELAY (LOFI)" onclick="addModule('DELAY (LOFI)',checked)"/><label for="checkbox">DELAY (LOFI)</label>
  <br>
  <input type="checkbox" id="DIODEFILTER" onclick="addModule('DIODEFILTER',checked)"/><label for="checkbox">DIODEFILTER</label>
  <br>
  <input type="checkbox" id="DRONE38" onclick="addModule('DRONE38',checked)"/><label for="checkbox">DRONE38</label>
  <br>
  <input type="checkbox" id="DRONX" onclick="addModule('DRONX',checked)"/><label for="checkbox">DRONX</label>
  <br>
  <input type="checkbox" id="DRUMKIT 010" onclick="addModule('DRUMKIT 010',checked)"/><label for="checkbox">DRUMKIT 010</label>
  <br>
  <input type="checkbox" id="FILTER (WASP TYPE)" onclick="addModule('FILTER (WASP TYPE)',checked)"/><label for="checkbox">FILTER (WASP TYPE)</label>
  <br>
  <input type="checkbox" id="FMOS" onclick="addModule('FMOS',checked)"/><label for="checkbox">FMOS</label>
  <br>
  <input type="checkbox" id="GRAINS" onclick="addModule('GRAINS',checked)"/><label for="checkbox">GRAINS</label>
  <br>
  <input type="checkbox" id="Wonkystuff&apos&#59;s BioT" onclick="addModule('Wonkystuff&apos;s BioT',checked)"/><label for="checkbox">Wonkystuff&apos;s BioT</label>
  <br>
  <input type="checkbox" id="JOYSTICK" onclick="addModule('JOYSTICK',checked)"/><label for="checkbox">JOYSTICK</label>
  <br>
  <input type="checkbox" id="KICK" onclick="addModule('KICK',checked)"/><label for="checkbox">KICK</label>
  <br>
  <input type="checkbox" id="Kurt&apos&#59;s Dead Band" onclick="addModule('Kurt&apos;s Dead Band',checked)"/><label for="checkbox">Kurt&apos;s Dead Band</label>
  <br>
  <input type="checkbox" id="Kurt&apos&#59;s Quad Boost" onclick="addModule('Kurt&apos;s Quad Boost',checked)"/><label for="checkbox">Kurt&apos;s Quad Boost</label>
  <br>
  <input type="checkbox" id="Kurt&apos&#59;s The Great Divide" onclick="addModule('Kurt&apos;s The Great Divide',checked)"/><label for="checkbox">Kurt&apos;s The Great Divide</label>
  <br>
  <input type="checkbox" id="Kurt&apos&#59;s Five steps" onclick="addModule('Kurt&apos;s Five steps',checked)"/><label for="checkbox">Kurt&apos;s Five steps</label>
  <br>
  <input type="checkbox" id="Kyaa&apos&#59;s Euclid Grid" onclick="addModule('Kyaa&apos;s Euclid Grid',checked)"/><label for="checkbox">Kyaa&apos;s Euclid Grid</label>
  <br>
  <input type="checkbox" id="LOGIC" onclick="addModule('LOGIC',checked)"/><label for="checkbox">LOGIC</label>
  <br>
  <input type="checkbox" id="LOPAG (VACTROL LOPASS GATE)" onclick="addModule('LOPAG (VACTROL LOPASS GATE)',checked)"/><label for="checkbox">LOPAG (VACTROL LOPASS GATE)</label>
  <br>
  <input type="checkbox" id="MIXCONSOLE" onclick="addModule('MIXCONSOLE',checked)"/><label for="checkbox">MIXCONSOLE</label>
  <br>
  <input type="checkbox" id="MIXER 4-4" onclick="addModule('MIXER 4-4',checked)"/><label for="checkbox">MIXER 4-4</label>
  <br>
  <input type="checkbox" id="MM-DIV" onclick="addModule('MM-DIV',checked)"/><label for="checkbox">MM-DIV</label>
  <br>
  <input type="checkbox" id="MODULATORS" onclick="addModule('MODULATORS',checked)"/><label for="checkbox">MODULATORS</label>
  <br>
  <input type="checkbox" id="MS20 FILTER" onclick="addModule('MS20 FILTER',checked)"/><label for="checkbox">MS20 FILTER</label>
  <br>
  <input type="checkbox" id="MULTIFX" onclick="addModule('MULTIFX',checked)"/><label for="checkbox">MULTIFX</label>
  <br>
  <input type="checkbox" id="NOISE" onclick="addModule('NOISE',checked)"/><label for="checkbox">NOISE</label>
  <br>
  <input type="checkbox" id="NYLE FILTER" onclick="addModule('NYLE FILTER',checked)"/><label for="checkbox">NYLE FILTER</label>
  <br>
  <input type="checkbox" id="OR 2x4" onclick="addModule('OR 2x4',checked)"/><label for="checkbox">OR 2x4</label>
  <br>
  <input type="checkbox" id="ORNAMENT & CRIME" onclick="addModule('ORNAMENT & CRIME',checked)"/><label for="checkbox">ORNAMENT & CRIME</label>
  <br>
  <input type="checkbox" id="PHASER" onclick="addModule('PHASER',checked)"/><label for="checkbox">PHASER</label>
  <br>
  <input type="checkbox" id="POLAMIX" onclick="addModule('POLAMIX',checked)"/><label for="checkbox">POLAMIX</label>
  <br>
  <input type="checkbox" id="QUANTIZER" onclick="addModule('QUANTIZER',checked)"/><label for="checkbox">QUANTIZER</label>
  <br>
  <input type="checkbox" id="SAMPLE & HOLD" onclick="addModule('SAMPLE & HOLD',checked)"/><label for="checkbox">SAMPLE & HOLD</label>
  <br>
  <input type="checkbox" id="SAWVOX" onclick="addModule('SAWVOX',checked)"/><label for="checkbox">SAWVOX</label>
  <br>
  <input type="checkbox" id="SEQ16" onclick="addModule('SEQ16',checked)"/><label for="checkbox">SEQ16</label>
  <br>
  <input type="checkbox" id="SEQ8" onclick="addModule('SEQ8',checked)"/><label for="checkbox">SEQ8</label>
  <br>
  <input type="checkbox" id="SLEW / EDGE" onclick="addModule('SLEW / EDGE',checked)"/><label for="checkbox">SLEW / EDGE</label>
  <br>
  <input type="checkbox" id="SOLINA" onclick="addModule('SOLINA',checked)"/><label for="checkbox">SOLINA</label>
  <br>
  <input type="checkbox" id="SPRINGREVERB" onclick="addModule('SPRINGREVERB',checked)"/><label for="checkbox">SPRINGREVERB</label>
  <br>
  <input type="checkbox" id="SVFILTER" onclick="addModule('SVFILTER',checked)"/><label for="checkbox">SVFILTER</label>
  <br>
  <input type="checkbox" id="SWITCHMATRIX 4x4" onclick="addModule('SWITCHMATRIX 4x4',checked)"/><label for="checkbox">SWITCHMATRIX 4x4</label>
  <br>
  <input type="checkbox" id="TBD" onclick="addModule('TBD',checked)"/><label for="checkbox">TBD</label>
  <br>
  <input type="checkbox" id="TOPOGRAF" onclick="addModule('TOPOGRAF',checked)"/><label for="checkbox">TOPOGRAF</label>
  <br>
  <input type="checkbox" id="TRIP" onclick="addModule('TRIP',checked)"/><label for="checkbox">TRIP</label>
  <br>
  <input type="checkbox" id="TRIQ164" onclick="addModule('TRIQ164',checked)"/><label for="checkbox">TRIQ164</label>
  <br>
  <input type="checkbox" id="VCO" onclick="addModule('VCO',checked)"/><label for="checkbox">VCO</label>
  <br>
  <input type="checkbox" id="WAVEFOLDER" onclick="addModule('WAVEFOLDER',checked)"/><label for="checkbox">WAVEFOLDER</label>
  <br>
  <input type="checkbox" id="WAVETABLES" onclick="addModule('WAVETABLES',checked)"/><label for="checkbox">WAVETABLES</label>
  <br>
  <input type="checkbox" id="Wonkystuff&apos&#59;s core1.ae" onclick="addModule('Wonkystuff&apos;s core1.ae',checked)"/><label for="checkbox">Wonkystuff&apos;s core1.ae</label>
  <br>
  <input type="checkbox" id="Wonkystuff&apos&#59;s mm33" onclick="addModule('Wonkystuff&apos;s mm33',checked)"/><label for="checkbox">Wonkystuff&apos;s mm33</label>
  <br>
  <input type="checkbox" id="Wonkystuff&apos&#59;s Moco" onclick="addModule('Wonkystuff&apos;s Moco',checked)"/><label for="checkbox">Wonkystuff&apos;s Moco</label>
  <br>
  <input type="checkbox" id="Wonkystuff&apos&#59;s QVCA" onclick="addModule('Wonkystuff&apos;s QVCA',checked)"/><label for="checkbox">Wonkystuff&apos;s QVCA</label>
  <br>
  <input type="checkbox" id="Wonkystuff&apos&#59;s RBSS" onclick="addModule('Wonkystuff&apos;s RBSS',checked)"/><label for="checkbox">Wonkystuff&apos;s RBSS</label>
  <br>
  <input type="checkbox" id="XMI" onclick="addModule('XMI',checked)"/><label for="checkbox">XMI</label>
  <br>
</div>
<div style="text-align: center;margin: auto;width: 99%;">
<h1 >AE MODULAR PATCH INSPIRATION</h1>
<div id="patches">
</div>

<button class="button button5" onclick="generatePatch()">NEW PATCH STARTER</button>
<br>
<div id="instructions">
</div>

<button class="button button5" onclick="generateInstruction()">NEW INSTRUCTION</button>
<br>

</div>
<button class="button button5" style="position: fixed;right: 0;bottom: 0;" onclick="deleteAll()">CLEAR</button>
<button class="button button5" style="position: fixed;right: 0;top: 0;" onclick="helppopupshow()">?</button>
<div id="helppopup" style="width: 33%;position: absolute;background-color: lightgrey; padding:10px;text-align: center;top: 50%;left: 50%; display: none;transform:translate(-50%, -50%);box-shadow: 0px 0px 25px 12px grey;border-style: solid;">
  <h2>HELP</h2>
  <p>HOW TO USE: On the left side, select the modules in your rack. Then, click on "NEW PATCH STARTER" to generate a patching challenge. If you wish, click "NEW INSTRUCTION" to generate a specific patching instruction. These are optimised to not generate invalid patches (eg. you can't patch the output of a 2LFO to SPRINGREVERB) but for some weird modules (like grains, which can change) it may not generate valid patches.</p>
  <p>WHAT TO DO: This is made to be used however you want. If you want to only generate instructions, go ahead! If you want to only select some of your modules, go ahead! I recommend not selecting mixer modules as you should probably just be able to patch that as you need.</p>
  <p>UPLOAD/DOWNLOAD: I realised that if you wanted to come back to the site, re-entering all of your modules would be tedious, so I added a method of saving your modules. The "download" button will download your currently selected modules as a .txt file, named modules.txt. On a later visit, you may press "choose file" and upload the modules.txt file. Then press "load selected file" and all your modules will be re-selected.</p>
  <p>FOOTNOTES: Thanks for visiting! I have only very occasionally dabbled in HTML/Javascript so this has been a learning experience. I hope you enjoy :)</p>
  <p>Made by Timothyjackman</p>
  <button class="button button5" onclick="helppopuphide()">CLOSE</button>
</div>

</body>
</html> 

