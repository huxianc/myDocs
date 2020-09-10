```html
<div id="cesiumContainer" class="fullSize"></div>
<div id="loadingOverlay"><h1>Loading...</h1></div>
<div id="toolbar"></div>
```

```css
@import url(../templates/bucket.css);
```

```js
var viewer = new Cesium.Viewer("cesiumContainer", {
  infoBox: false,
  selectionIndicator: false,
  shadows: true,
  shouldAnimate: true,
});

function createModel(url, height) {
  viewer.entities.removeAll();

  // Cartesian3 3d 笛卡尔坐标
  // fromDegrees 从以度为单位的经度和纬度值返回Cartesian3位置。
  var position = Cesium.Cartesian3.fromDegrees(
    -123.0744619,
    44.0503706,
    height
  );
  // toRadians 将角度转换为弧度
  var heading = Cesium.Math.toRadians(135);
  var pitch = 0;
  var roll = 0;
  // new Cesium.HeadingPitchRoll ( heading , pitch , roll )
  // 旋转表示为航向，俯仰和横滚。标题是围绕负Z轴。节距是绕负y轴的旋转。滚动是关于正x轴。
  var hpr = new Cesium.HeadingPitchRoll(heading, pitch, roll);
  // Transforms 包含用于将位置转换为各种参考系的功能。
  // headingPitchRollQuaternion 根据参考系计算四元数，其中参考系具有根据航向-俯仰-横滚角计算的轴以提供的原点为中心。航向是当地北部的旋转正角向东增加的方向。俯仰是从本地东西向平面的旋转。正俯仰角在飞机上方。负俯仰角在平面下方。横摇是绕局部东轴应用的第一次旋转。
  var orientation = Cesium.Transforms.headingPitchRollQuaternion(position, hpr);

  var entity = viewer.entities.add({
    name: url,
    position: position,
    orientation: orientation,
    model: {
      uri: url,
      minimumPixelSize: 128,
      maximumScale: 20000,
    },
  });
  // trackedEntity 获取或设置相机当前正在跟踪的Entity实例。
  viewer.trackedEntity = entity;
}

var options = [
  {
    text: "Aircraft",
    onselect: function () {
      createModel("../../SampleData/models/CesiumAir/Cesium_Air.glb", 5000.0);
    },
  },
  {
    text: "Ground Vehicle",
    onselect: function () {
      createModel("../../SampleData/models/GroundVehicle/GroundVehicle.glb", 0);
    },
  },
  {
    text: "Hot Air Balloon",
    onselect: function () {
      createModel(
        "../../SampleData/models/CesiumBalloon/CesiumBalloon.glb",
        1000.0
      );
    },
  },
  {
    text: "Milk Truck",
    onselect: function () {
      createModel(
        "../../SampleData/models/CesiumMilkTruck/CesiumMilkTruck.glb",
        0
      );
    },
  },
  {
    text: "Skinned Character",
    onselect: function () {
      createModel("../../SampleData/models/CesiumMan/Cesium_Man.glb", 0);
    },
  },
  {
    text: "Draco Compressed Model",
    onselect: function () {
      createModel(
        "../../SampleData/models/DracoCompressed/CesiumMilkTruck.gltf",
        0
      );
    },
  },
];

Sandcastle.addToolbarMenu(options);
```
