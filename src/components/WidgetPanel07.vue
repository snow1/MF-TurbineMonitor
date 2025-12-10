<template>
  <LayoutPanel>
    <div class="container">
      <div class="item" v-for="item in list">
        <div class="item-label">{{ item.label }}</div>
        <div class="item-value">{{ item.value }}{{ item.unit }}</div>
      </div>
    </div>
  </LayoutPanel>
</template>
<script setup lang="ts">
import { LayoutPanel } from '@/layout'
import { computed } from 'vue'

interface PropsType {
  name: string
}
const props = defineProps<PropsType>()

const CONFIG: any = {
  PitchSystem: [
    { label: ' Pitch Angle', value: 15, unit: '°' },
    { label: 'Pitch Speed', value: 2, unit: '°/s' },
    { label: 'Pitch System Temperature', value: 45, unit: '°C' },
    { label: 'Motor Load', value: 3.5, unit: 'kW' },
    { label: 'Pitch Position Sensor Feedback', value: 1.2, unit: 'm' },
    { label: 'Fault Status', value: 0, unit: '(No Fault)' },
    { label: 'Power Voltage', value: 400, unit: 'V' },
    { label: 'Blade Pressure', value: 1200, unit: 'Pa' },
    { label: 'Pitch Angle Change', value: 0.5, unit: '°' },
    { label: 'Pitch Response Time', value: 0.1, unit: 's' },
    { label: 'Current', value: 10, unit: 'A' },
    { label: 'Pitch System Running Time', value: 200, unit: 'h' },
    { label: 'Pitch Fault Count', value: 1, unit: '' },
    { label: 'System Working Status', value: 'Normal', unit: '' },
    { label: 'Pitch Motor Temperature', value: 60, unit: '°C' },
    { label: 'Pitch Angle Limit', value: 25, unit: '°' },
  ],
  Rotor: [
    { label: 'Rotor Diameter', value: 120, unit: 'm' },
    { label: 'Rotor Weight', value: 15000, unit: 'kg' },
    { label: 'Rotor Material', value: 'Glass Fiber', unit: '' },
    { label: 'Rotor Speed', value: 12, unit: 'r/min' },
    { label: 'Maximum Load', value: 5000, unit: 'N' },
    { label: 'Rotor Tilt Angle', value: 5, unit: '°' },
    { label: 'Rotor Lifetime', value: 20, unit: 'year' },
    { label: 'Rotor Aerodynamic Efficiency', value: 92, unit: '%' },
    { label: 'Rotor Temperature', value: 50, unit: '°C' },
    { label: 'Rotor Material Strength', value: 350, unit: 'MPa' },
    { label: 'Rotor Vibration Frequency', value: 60, unit: 'Hz' },
    { label: 'Rotor Rotational Inertia', value: 150, unit: 'kg·m²' },
    { label: 'Rotor Working Time', value: 1000, unit: 'h' },
    { label: 'Rotor Maintenance Cycle', value: 5, unit: 'year' },
    { label: 'Rotor Friction Coefficient', value: 0.02, unit: '' },
    { label: 'Rotor Cooling Method', value: 'Air Cooling', unit: '' },
  ],
  MainShaft: [
    { label: 'Main Shaft Diameter', value: 0.15, unit: 'm' },
    { label: 'Main Shaft Length', value: 5.0, unit: 'm' },
    { label: 'Main Shaft Material', value: 'Steel', unit: '' },
    { label: 'Main Shaft Weight', value: 2000, unit: 'kg' },
    { label: 'Main Shaft Speed', value: 15, unit: 'r/min' },
    { label: 'Main Shaft Bearing Capacity', value: 10000, unit: 'N' },
    { label: 'Main Shaft Temperature', value: 60, unit: '°C' },
    { label: 'Main Shaft Bearing Type', value: 'Rolling Bearing', unit: '' },
    { label: 'Main Shaft Material Strength', value: 500, unit: 'MPa' },
    { label: 'Main Shaft Working Time', value: 3000, unit: 'h' },
    { label: 'Main Shaft Wear Degree', value: 0.1, unit: 'mm' },
    { label: 'Main Shaft Dynamic Balance Status', value: 'Normal', unit: '' },
    { label: 'Main Shaft Cooling Method', value: 'Oil Cooling', unit: '' },
    { label: 'Main Shaft Installation Angle', value: 0, unit: '°' },
    { label: 'Main Shaft Maintenance Cycle', value: 3, unit: 'year' },
    { label: 'Main Shaft Vibration Frequency', value: 50, unit: 'Hz' },
  ],
  Gearbox: [
    { label: 'Gearbox Type', value: 'Planetary Gearbox', unit: '' },
    { label: 'Gearbox Ratio', value: 15, unit: ':1' },
    { label: 'Gearbox Input Speed', value: 20, unit: 'r/min' },
    { label: 'Gearbox Output Speed', value: 300, unit: 'r/min' },
    { label: 'Gearbox Efficiency', value: 95, unit: '%' },
    { label: 'Gearbox Temperature', value: 70, unit: '°C' },
    { label: 'Gearbox Weight', value: 250, unit: 'kg' },
    { label: 'Gearbox Material', value: 'Alloy Steel', unit: '' },
    { label: 'Gearbox Noise Level', value: 60, unit: 'dB' },
    { label: 'Gearbox Lubrication Method', value: 'Oil Lubrication', unit: '' },
    { label: 'Gearbox Wear Degree', value: 0.05, unit: 'mm' },
    { label: 'Gearbox Maintenance Cycle', value: 4, unit: 'year' },
    { label: 'Gearbox Cooling Method', value: 'Water Cooling', unit: '' },
    { label: 'Gearbox Load Capacity', value: 20000, unit: 'N' },
    { label: 'Gearbox Working Time', value: 5000, unit: 'h' },
    { label: 'Gearbox Vibration Status', value: 'Normal', unit: '' },
  ],
  油冷装置: [
    { label: 'Oil Cooler Type', value: 'Plate Cooler', unit: '' },
    { label: 'Oil Flow', value: 50, unit: 'L/min' },
    { label: 'Oil Temperature', value: 40, unit: '°C' },
    { label: 'Cooling Efficiency', value: 90, unit: '%' },
    { label: 'Oil Cooler Weight', value: 100, unit: 'kg' },
    { label: 'Oil Type', value: 'Synthetic Oil', unit: '' },
    { label: 'Cooling Media Temperature', value: 25, unit: '°C' },
    { label: 'Maximum Working Pressure', value: 5, unit: 'bar' },
    { label: 'Oil Cooler Working Time', value: 2000, unit: 'h' },
    { label: 'Oil Cooler Fault Count', value: 0, unit: '' },
    { label: 'Oil Flow Fluctuation', value: 5, unit: 'L/min' },
    { label: 'Oil Cooler Material', value: 'Aluminum Alloy', unit: '' },
    { label: 'Oil Cooler Maintenance Cycle', value: 3, unit: 'year' },
    { label: 'Work Noise', value: 55, unit: 'dB' },
    { label: 'Cooler Vibration Status', value: 'Normal', unit: '' },
    { label: 'Oil Temperature Upper Limit', value: 70, unit: '°C' },
  ],
  偏航电机: [
    { label: 'Motor Type', value: 'Servo Motor', unit: '' },
    { label: 'Rated Power', value: 5, unit: 'kW' },
    { label: 'Rated Voltage', value: 400, unit: 'V' },
    { label: 'Rated Speed', value: 1500, unit: 'r/min' },
    { label: 'Maximum Torque', value: 30, unit: 'N·m' },
    { label: 'Motor Weight', value: 50, unit: 'kg' },
    { label: 'Control Type', value: 'Closed Loop Control', unit: '' },
    { label: 'Working Temperature', value: 70, unit: '°C' },
    { label: 'Motor Running Time', value: 1000, unit: 'h' },
    { label: 'Motor Fault Status', value: 0, unit: '(No Fault)' },
    { label: 'Motor Start-up Count', value: 10, unit: '' },
    { label: 'Motor Efficiency', value: 92, unit: '%' },
    { label: 'Motor Cooling Method', value: 'Air Cooling', unit: '' },
    { label: 'Motor Insulation Level', value: 'F Level', unit: '' },
    { label: 'Motor Load Status', value: 'Normal', unit: '' },
    { label: 'Motor Vibration Status', value: 'Normal', unit: '' },
  ],
  风冷装置: [
    { label: 'Cooler Type', value: 'Air Cooler', unit: '' },
    { label: 'Fan Type', value: 'Axial Fan', unit: '' },
    { label: 'Fan Power', value: 1.5, unit: 'kW' },
    { label: 'Fan Flow', value: 3000, unit: 'm³/h' },
    { label: 'Cooling Efficiency', value: 85, unit: '%' },
    { label: 'Working Temperature', value: 35, unit: '°C' },
    { label: 'Cooler Weight', value: 25, unit: 'kg' },
    { label: 'Fan Speed', value: 1200, unit: 'r/min' },
    { label: 'Fan Running Time', value: 1500, unit: 'h' },
    { label: 'Fan Fault Status', value: 0, unit: '(No Fault)' },
    { label: 'Cooler Noise Level', value: 50, unit: 'dB' },
    { label: 'Fan Material', value: 'Plastic', unit: '' },
    { label: 'Cooler Maintenance Cycle', value: 2, unit: 'year' },
    { label: 'Fan Vibration Status', value: 'Normal', unit: '' },
    { label: 'Fan Current', value: 3, unit: 'A' },
    { label: 'Fan Flow Fluctuation', value: 100, unit: 'm³/h' },
  ],
  发电机: [
    { label: 'Generator Type', value: 'Synchronous Generator', unit: '' },
    { label: 'Rated Power', value: 1000, unit: 'kW' },
    { label: 'Rated Voltage', value: 400, unit: 'V' },
    { label: 'Rated Frequency', value: 50, unit: 'Hz' },
    { label: 'Efficiency', value: 95, unit: '%' },
    { label: 'Generator Weight', value: 500, unit: 'kg' },
    { label: 'Generator Speed', value: 1500, unit: 'r/min' },
    { label: 'Cooling Method', value: 'Water Cooling', unit: '' },
    { label: 'Generator Running Time', value: 2000, unit: 'h' },
    { label: 'Generator Fault Status', value: 0, unit: '(No Fault)' },
    { label: 'Generator Start-up Count', value: 10, unit: '' },
    { label: 'Generator Output Current', value: 1500, unit: 'A' },
    { label: 'Generator Maintenance Cycle', value: 4, unit: 'year' },
    { label: 'Generator Vibration Status', value: 'Normal', unit: '' },
    { label: 'Generator Temperature', value: 70, unit: '°C' },
    { label: 'Generator Load Status', value: 'Normal', unit: '' },
  ],
  控制柜: [
    { label: 'Control Cabinet Type', value: 'Power Distribution Control Cabinet', unit: '' },
    { label: 'Rated Voltage', value: 400, unit: 'V' },
    { label: 'Rated Current', value: 100, unit: 'A' },
    { label: 'Protection Level', value: 'IP65', unit: '' },
    { label: 'Control Method', value: 'Automatic Control', unit: '' },
    { label: 'Control Cabinet Material', value: 'Cold Rolled Steel', unit: '' },
    { label: 'Control Cabinet Weight', value: 150, unit: 'kg' },
    { label: 'Working Temperature', value: 40, unit: '°C' },
    { label: 'Control Cabinet Working Status', value: 'Normal', unit: '' },
    { label: 'Control Cabinet Temperature', value: 50, unit: '°C' },
    { label: 'Control Cabinet Project Count', value: 20, unit: '' },
    { label: 'Control Cabinet Maintenance Cycle', value: 3, unit: 'year' },
    { label: 'Control Cabinet Vibration Status', value: 'Normal', unit: '' },
    { label: 'Control Cabinet Protection Level Test', value: 'Pass', unit: '' },
  ],
}

const list = computed(() => {
  return CONFIG[props.name] || []
})
</script>

<style lang="scss" scoped>
.container {
  display: grid;
  grid-template-rows: repeat(4, 1fr);
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 10px;
  height: 100%;
  overflow: hidden;
  .item {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background-color: rgba(93, 101, 122, 20%);
    .item-label {
      font-size: 12px;
    }
    .item-value {
      margin-top: 4px;
      font-size: 12px;
      color: #74f7fd;
    }
  }
}
</style>
