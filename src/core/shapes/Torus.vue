<script setup lang="ts">
import { TresColor } from '@tresjs/core'
import { TorusGeometry } from 'three'
import { shallowRef } from 'vue'

export type TorusProps = {
  /**
   * The radius, tube, radialSegments, tubularSegments, arc of the torus.
   * @default [1, 1, 16, 80, Math.PI * 2]
   * @type {number[]}
   * @memberof TorusProps
   * @see https://threejs.org/docs/#api/en/geometries/TorusGeometry
   */
  args?: ConstructorParameters<typeof TorusGeometry>
  /**
   * The color of the torus.
   * @default 0xffffff
   * @type {TresColor}
   * @memberof TorusProps
   * @see https://threejs.org/docs/#api/en/materials/MeshBasicMaterial
   */
  color?: TresColor
}

// TODO: remove disable once eslint is updated to support vue 3.3
// eslint-disable-next-line vue/no-setup-props-destructure
const { args = [1, 1, 16, 80], color = '0xffffff' } = defineProps<TorusProps>()

const torusRef = shallowRef()

defineExpose({
  value: torusRef,
})
</script>
<template>
  <TresMesh ref="torusRef" v-bind="$attrs">
    <TresTorusGeometry :args="args" />
    <slot>
      <TresMeshBasicMaterial :color="color" />
    </slot>
  </TresMesh>
</template>
