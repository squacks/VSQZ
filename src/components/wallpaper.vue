<template>
<!-- 
  shouts out to al-ro for the webgl canvas BG:
  https://codepen.io/al-ro/pen/dEmvyy 
-->
  <div class="wallpaper">
    <canvas id="canvas" width="1400" height="600"></canvas>
    <!-- <canvas id="wallpaper" width="1400" height="600"></canvas> -->
  </div>
</template>

<script>
export default{
  mounted () {
    this.runWebGL()
  },
  methods: {
    runWebGL(){
      var canvas = document.getElementById("canvas");

      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;

      // Initialize the GL context
      var gl = canvas.getContext('webgl');
      if(!gl){
        console.error("Unable to initialize WebGL.");
      }

      //Time
      var time = 0.0;

      //************** Shader sources **************

      var vertexSource = `
      attribute vec2 position;
      void main() {
        gl_Position = vec4(position, 0.4, 0.7);
      }
      `;

      //Replace with GLSL fragment shader code
      var fragmentSource = `
      precision highp float;

      uniform float width;
      uniform float height;
      vec2 resolution = vec2(width, height);

      uniform float time;

      void main(){
        gl_FragColor = vec4(gl_FragCoord.xy/resolution, 0.2+0.3*sin(time), 0.2);
      }
      `;

      //************** Utility functions **************

      window.addEventListener( 'resize', onWindowResize, false );

      function onWindowResize(){
        canvas.width  = window.innerWidth;
        canvas.height = window.innerHeight;
        gl.viewport(0, 0, canvas.width, canvas.height);
        gl.uniform1f(widthHandle, window.innerWidth);
        gl.uniform1f(heightHandle, window.innerHeight);
      }

      //Compile shader and combine with source
      function compileShader(shaderSource, shaderType){
        var shader = gl.createShader(shaderType);
        gl.shaderSource(shader, shaderSource);
        gl.compileShader(shader);
        if(!gl.getShaderParameter(shader, gl.COMPILE_STATUS)){
          throw "Shader compile failed with: " + gl.getShaderInfoLog(shader);
        }
        return shader;
      }

      //From https://codepen.io/jlfwong/pen/GqmroZ
      //Utility to complain loudly if we fail to find the attribute/uniform
      function getAttribLocation(program, name) {
        var attributeLocation = gl.getAttribLocation(program, name);
        if (attributeLocation === -1) {
          throw 'Cannot find attribute ' + name + '.';
        }
        return attributeLocation;
      }

      function getUniformLocation(program, name) {
        var attributeLocation = gl.getUniformLocation(program, name);
        if (attributeLocation === -1) {
          throw 'Cannot find uniform ' + name + '.';
        }
        return attributeLocation;
      }

      //************** Create shaders **************

      //Create vertex and fragment shaders
      var vertexShader = compileShader(vertexSource, gl.VERTEX_SHADER);
      var fragmentShader = compileShader(fragmentSource, gl.FRAGMENT_SHADER);

      //Create shader programs
      var program = gl.createProgram();
      gl.attachShader(program, vertexShader);
      gl.attachShader(program, fragmentShader);
      gl.linkProgram(program);

      gl.useProgram(program);

      //Set up rectangle covering entire canvas 
      var vertexData = new Float32Array([
        -1.0,  1.0, 	// top left
        -1.0, -1.0, 	// bottom left
        1.0,  1.0, 	// top right
        1.0, -1.0, 	// bottom right
      ]);

      //Create vertex buffer
      var vertexDataBuffer = gl.createBuffer();
      gl.bindBuffer(gl.ARRAY_BUFFER, vertexDataBuffer);
      gl.bufferData(gl.ARRAY_BUFFER, vertexData, gl.STATIC_DRAW);

      // Layout of our data in the vertex buffer
      var positionHandle = getAttribLocation(program, 'position');

      gl.enableVertexAttribArray(positionHandle);
      gl.vertexAttribPointer(positionHandle,
        2, 				// position is a vec2 (2 values per component)
        gl.FLOAT, // each component is a float
        false, 		// don't normalize values
        2 * 4, 		// two 4 byte float components per vertex (32 bit float is 4 bytes)
        0 				// how many bytes inside the buffer to start from
        );

      //Set uniform handle
      var timeHandle = getUniformLocation(program, 'time');
      var widthHandle = getUniformLocation(program, 'width');
      var heightHandle = getUniformLocation(program, 'height');

      gl.uniform1f(widthHandle, window.innerWidth);
      gl.uniform1f(heightHandle, window.innerHeight);

      var lastFrame = Date.now();
      var thisFrame;

      function draw(){
        
        //Update time
        thisFrame = Date.now();
        time += (thisFrame - lastFrame)/1100;	
        lastFrame = thisFrame;

          
        //Send uniforms to program
        gl.uniform1f(timeHandle, time);
        
        //Draw a triangle strip connecting vertices 0-4
        gl.drawArrays(gl.TRIANGLE_STRIP, 0, 4);

        requestAnimationFrame(draw);
      }

      draw();
    }
  }
}


</script>

<style lang="scss">
.wallpaper {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: linear-gradient(160deg, #f9d7cf 10%, #ffb180);
  z-index: -1;
  // opacity: 0.5;
}
</style>
