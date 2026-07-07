<script lang="ts">
  import {
    getShaderColorFromString,
    ShaderFitOptions,
    ShaderMount,
    wavesFragmentShader
  } from '@paper-design/shaders';

  let { class: className = '' } = $props<{ class?: string }>();

  function shaderStrip(node: HTMLDivElement) {
    const mount = new ShaderMount(
      node,
      wavesFragmentShader,
      {
        u_colorFront: getShaderColorFromString('#95d3c1'),
        u_colorBack: getShaderColorFromString('#003229'),
        u_shape: 2,
        u_frequency: 1.7,
        u_amplitude: 0.38,
        u_spacing: 0.3,
        u_proportion: 0.54,
        u_softness: 0.72,
        u_fit: ShaderFitOptions.cover,
        u_scale: 1.2,
        u_rotation: 8,
        u_originX: 0.5,
        u_originY: 0.5,
        u_offsetX: 0,
        u_offsetY: 0,
        u_worldWidth: 320,
        u_worldHeight: 48
      },
      { alpha: true, antialias: true },
      0,
      1400,
      1,
      120000
    );

    return {
      destroy: () => mount.dispose()
    };
  }
</script>

<div
  use:shaderStrip
  class={`absolute inset-0 overflow-hidden rounded-[inherit] bg-linear-to-r from-(--primary) to-(--primary-fixed-dim) [&_canvas]:block [&_canvas]:h-full [&_canvas]:w-full ${className}`}
  aria-hidden="true"
></div>
