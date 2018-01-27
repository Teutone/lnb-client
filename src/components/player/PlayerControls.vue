<script>
  import { secondsToString } from '../../utility';
  import VolumeBar from './VolumeBar';

  export default {
    props: {
      status: { type: String, required: true },
      muted: { type: Boolean, required: true },
      volume: { type: Number, required: true },
      duration: { type: Number, required: true },
      currentTime: { type: Number, required: true },
    },

    components: {
      VolumeBar,
    },

    computed: {
      timeString() {
        return secondsToString(this.currentTime);
      },
      totalTimeString() {
        return secondsToString(this.duration);
      },
    },
  };
</script>
<template>
  <div class="player-controls">
    <button
      title="Previous [Left Arrow]"
      @click.prevent="$emit('previous')"
      class="icon-button"
    >
      <span class="iconicstroke-first"></span>
    </button>
    <button
      title="Play / Pause [Spacebar]"
      @click.prevent="$emit('toggle-play-pause')"
      class="icon-button"
    >
      <span v-if="status === 'paused'" class="iconicstroke-play"></span>
      <span v-if="status === 'playing'" class="iconicstroke-pause"></span>
      <span v-if="status === 'buffering'" class="iconicstroke-spin-alt ani-spin"></span>
    </button>
    <button
      title="Next [Right Arrow]"
      @click.prevent="$emit('next')"
      class="icon-button"
    >
      <span class="iconicstroke-last"></span>
    </button>

    <volume-bar
      :muted="muted"
      :volume="volume"
      @mute="$emit('mute', $event)"
      @volume="$emit('volume', $event)"
    ></volume-bar>

    <span class="player-controls__time">
      {{ timeString }} / {{ totalTimeString }}
    </span>
  </div>
</template>