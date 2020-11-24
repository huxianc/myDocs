<!--
 * @Description:
 * @Author: huxianc
 * @Date: 2020-11-24 10:38:30
 * @LastEditors: huxianc
 * @LastEditTime: 2020-11-24 10:39:59
-->

```js
import { mapState, mapMutations } from 'vuex'

computed:{
  ...mapState({
      mapObj: state => state.canvas.mapObj,
      mapId: state => state.canvas.mapId
    })
},
methods:{
  ...mapMutations('canvas', {
      setMapObj: 'SET_MAPOBJ',
      setMapId: 'SET_MAPID'
    }),
}
```
