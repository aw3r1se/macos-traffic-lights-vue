# MacOS Traffic Lights Vue Component

Based on <a href="https://github.com/aw3r1se/macOS-traffic-lights">aw3r1se/macOS-traffic-lights</a>, if you need just svg files, check it first

## 🔧 Installation

```sh
npm i macos-traffic-lights-vue
```

## ✏️ Usage

```vue
<script>
  import TrafficLights from 'macos-traffic-lights-vue';
</script>

<template>
  <TrafficLights 
      @close="handleClose"
      @minimize="handleMinimize"
      @maximize="handleMaximize"
  />
</template>
```

If you need to focus/unfocus the buttons, you can use the following functions:
```vue
<script>
  import { ref } from 'vue';
  import trafficLights from 'macos-traffic-lights-vue';
  
  const trafficLights = ref();
  
  const someFunction = () => {
      if (x) {
          trafficLights.value.focus();
      }
      
      if (y) {
          trafficLights.value.unfocus();
      }
  };
</script>

<template>
  <TrafficLights
      ref="trafficLights"
      @close="handleClose"
      @minimize="handleMinimize"
      @maximize="handleMaximize"
  />
</template>
```

## 🤝 Contributing
If you want to add or improve something - you are welcome

* Fork → Branch → Commit with feat: / fix: prefix
* Test locally
* Open a pull request