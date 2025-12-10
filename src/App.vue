<template>
  <Layout :loading="loading">
    <template #left>
      <WidgetPanel04 title="Parameter Monitoring" />
      <WidgetPanel02 title="Historical Power" />
      <WidgetPanel03 title="Daily Generation Monitoring" />
    </template>
    <template #right>
      <WidgetPanel07
        v-show="current"
        :title="current + ' Details'"
        :name="current"
      />
      <WidgetPanel06 v-show="!current" title="Operation Monitoring" />
      <WidgetPanel01 title="Fault Comparison" />
      <WidgetPanel05 title="Yaw Angle Monitoring" />
    </template>
    <template #middle>
      <div style="width: 100%; height: 100%" ref="container"></div>
    </template>
  </Layout>
</template>
<script setup lang="ts">
import {
  WidgetPanel01,
  WidgetPanel02,
  WidgetPanel03,
  WidgetPanel04,
  WidgetPanel05,
  WidgetPanel06,
  WidgetPanel07,
} from '@/components'
import { provide } from 'vue'
import { Layout } from '@/layout'
import { useTurbine } from '@/hooks'
const {
  container,
  loading,
  current,
  eqDecomposeAnimation,
  eqComposeAnimation,
  startWarning,
  stopWarning,
} = useTurbine()

provide('events', {
  eqDecomposeAnimation,
  eqComposeAnimation,
  startWarning,
  stopWarning,
})
</script>
