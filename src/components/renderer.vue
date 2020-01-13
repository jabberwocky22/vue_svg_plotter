<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>Enter codes in terminal below to draw your patterns!</p>
    <section id="codeArea">
      <SvgInput @getAttributes="getAttributes"></SvgInput>
      <div class="divider"></div>
      <svg width="250" height="250">
        <g v-html="shapes" />
      </svg>
    </section>
    <section
      id="errorArea"
      :class="errorCollector.length>0 ? 'display' : 'hide'"
    >{{errorCollector.toString()}}</section>
  </div>
</template>

<script>
import SvgInput from "./Input";

export default {
  name: "HelloWorld",
  props: {
    msg: String
  },
  data() {
    return {
      shapes: "",
      color: "",
      errorCollector: ""
    };
  },
  components: {
    SvgInput
  },
  methods: {
    getAttributes(input) {
      this.shapes = "";
      this.errorCollector = "";
      for (let i = 0; i < input.length; i++) {
        this.color = [
          Math.floor(Math.random() * 256),
          Math.floor(Math.random() * 256),
          Math.floor(Math.random() * 256)
        ];
        const element = input[i];
        let eachAttribute = element.split(" ");
        const geomShape = eachAttribute[0];

        switch (geomShape.toLowerCase()) {
          case "c": {
            // code block
            let cx = eachAttribute[1],
              cy = eachAttribute[2],
              r = eachAttribute[3];
            this.errorCollector = checkUndefined(
              ["cx", "cy", "r"],
              [cx, cy, r],
              i
            );
            if (this.errorCollector.length > 0) {
              return;
            }
            this.shapes += `<circle cx="${cx}" cy="${cy}" r="${r}" fill="rgb(${this.color.toString()})"/>`;
            break;
          }

          case "r": {
            // code block
            let x = eachAttribute[1],
              y = eachAttribute[2],
              width = eachAttribute[3],
              height = eachAttribute[4];
            this.errorCollector = checkUndefined(
              ["x", "y", "width", "height"],
              [x, y, width, height],
              i
            );
            if (this.errorCollector.length > 0) {
              return;
            }
            this.shapes += `<rect x="${x}" y="${y}" width="${width}" height="${height}" fill="rgb(${this.color.toString()})"/>`;
            break;
          }

          case "l": {
            // code block
            let x1 = eachAttribute[1],
              y1 = eachAttribute[2],
              x2 = eachAttribute[3],
              y2 = eachAttribute[4],
              stroke = eachAttribute[5];
            this.errorCollector = checkUndefined(
              ["x1", "y1", "x2", "y2", "stroke"],
              [x1, y1, x2, y2, stroke],
              i
            );
            if (this.errorCollector.length > 0) {
              return;
            }
            this.shapes += `<line x1="${x1}" y1="${y1}" x2="${x2}" y2="${y2}" style="stroke:rgb(${this.color.toString()});stroke-width:${stroke}"/>`;
            break;
          }

          case "p": {
            // code block
            eachAttribute.splice(0, 1);
            for (let j = 0; j < eachAttribute.length; j++) {
              const coordinateSet = eachAttribute[j];
              if (coordinateSet.split(",").length !== 2) {
                this.errorCollector = `polygon is mis-defined @ Line ${i + 1} `;
                return;
              }
            }
            const coordinates = eachAttribute.toString();
            this.shapes += `<polygon points="${coordinates}" fill="rgb(${this.color.toString()})"/>`;
            break;
          }

          default:
            // code block
            this.errorCollector = `Please enter valid codes @ Line ${i + 1} `;
            return;
        }
      }
      function checkUndefined(indexArr, array, lineNum) {
        let errors = [];
        for (let i = 0; i < array.length; i++) {
          if (array[i] === undefined || array[i] === "" || array[i] === null) {
            errors.push(`${indexArr[i]} is undefined @ Line ${lineNum + 1} `);
          }
        }
        if (errors.length === 0) {
          return "";
        }
        return errors;
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.display {
  display: block;
}
.hide {
  display: none;
}
#codeArea {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  align-items: center;
  width: 80vw;
  margin: auto;
}
#errorArea {
  width: 330px;
  height: 90px;
  position: absolute;
  top: 2px;
  right: 2px;
  border-radius: 0.2em;
  background: pink;
  color: crimson;
  text-align: left;
  padding: 6px 10px;
}
.divider {
  border-left: 3px solid #ccc;
  height: 500px;
}
svg {
  box-sizing: border-box;
  border: solid;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
