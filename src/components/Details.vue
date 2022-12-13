<template>
  <div class="details">
    <p>Details</p>
    <ul>
    
      <li v-for="(player, index) in dmglist" v-bind:key="index" :class="player.class">
      {{player.name}} <span class="total-dmg">({{totalDamage}} dmg) {{dps}} dps</span>
    </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Details',
  data: function(){
    return {
      dmglist: [
      {'name': 'Benkt', 'class' : 'shaman','damage' : 0 ,'dps': 0}
      ],
      spells: [],
      totalDamage: 0,
      startTime: 0,
      dps: 0,
    }
  },
  watch: {
    spells : {
      handler(newVal){
        let dmg = 0;
        for (const element of newVal) {
          dmg = dmg + element.number;
        }
        this.totalDamage = dmg;
      },
      deep: true
    }
  },
  methods : {
    calculateDps: function(){
      let now = Math.floor(Date.now() / 1000)+1;
      const diff = now - this.startTime;
      this.dps = Math.floor(this.totalDamage/diff);
    }
  },
  mounted() {
    
    let _this = this;
        document.addEventListener("click", function(event){
          if(_this.startTime === 0){
            _this.startTime = Math.floor(Date.now() / 1000)
          }
        
          setInterval(function() {
           _this.calculateDps()
          }, 500);

          let clickY = event.clientY
          let clickX = event.clientX      

          const newDiv = document.createElement("div");
          let randomOffset = Math.floor(Math.random()*100);
          newDiv.style.position = 'fixed';
          newDiv.style.left = `${clickX-50+randomOffset}px`;
          newDiv.style.top = `${clickY-20}px`;
          newDiv.style.color = 'yellow'
          newDiv.classList.add("chainlightning-dmg");
          let dmgNumber = Math.floor(Math.random()*2000+2000);
          let obj = {'spell' : 'Chain Lightning', 'number': dmgNumber};
          _this.spells.push(obj);
          const newContent = document.createTextNode(dmgNumber);
          newDiv.appendChild(newContent);
          document.body.appendChild(newDiv);
          setTimeout(function(){
            newDiv.parentNode.removeChild(newDiv);
          }, 2000)
          
      });
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.details {
  background: #000;
  color: #fff;
  padding: 10px 10px;
  display: inline-block;
  position: fixed;
  bottom: 0px;
  right: 10px;
  min-width: 280px;
}
p {
  margin: 0px;
}
ul {
  list-style: none;
  padding-left: 0px;
}
li {
  padding: 2px 10px;
  margin-bottom: 5px;
}
li.shaman {
  background: blue;
  color: white;
}
.total-dmg {
  text-align: right;
  float: right;
  font-size: 12px;
}
.chainlightning-dmg {
  animation-name: scrollup;
  animation-duration: 2.1s;
  font-size: 24px;  
}
@keyframes scrollup {
  from {margin-top: 0px;}
  to {margin-top: -70px;}
}

</style>
