<script setup lang="ts">
import 'leaflet/dist/leaflet.css';
import { onMounted, ref } from 'vue';
import L from 'leaflet';
const mapContainer = ref(null);
onMounted(() => {
  // 初始化地图
  const map = L.map(mapContainer.value).setView([51.505, -0.09], 13);

  // 加载底图
  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
  }).addTo(map);

  // 添加标记
  const marker = L.marker([51.5, -0.09]).addTo(map);
  marker.bindPopup('<b>Hello world!</b><br />I am a popup.').openPopup();

  // 添加圆形
  const circle = L.circle([51.508, -0.11], {
    color: 'red',
    fillColor: '#f03',
    fillOpacity: 0.5,
    radius: 500
  }).addTo(map);
  circle.bindPopup('I am a circle.');

  // 添加多边形
  const polygon = L.polygon([
    [51.509, -0.08],
    [51.503, -0.06],
    [51.51, -0.047]
  ]).addTo(map);
  polygon.bindPopup('I am a polygon.');

  // 点击事件
  map.on('click', (e) => {
    L.popup()
      .setLatLng(e.latlng)
      .setContent(`You clicked the map at ${e.latlng.toString()}`)
      .openOn(map);
  });
});
</script>

<template>
  <div id="map" ref="mapContainer" style="width: 100%; height: 100vh;"></div>
</template>

<style scoped>

</style>
