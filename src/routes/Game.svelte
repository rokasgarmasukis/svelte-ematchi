<script lang="ts">
  import Grid from './Grid.svelte';
  import { levels } from './levels';
  import type { Level } from './levels';

  const level = levels[0];
  let size: number = level.size;
  let grid: string[] = create_grid(level);
  let found: string[] = [];

  function create_grid(level: Level): string[] {
    const copy = level.emojis.slice();
    const pairs: string[] = [];

    for (let i = 0; i < (level.size * level.size) / 2; i++) {
      const index = Math.floor(Math.random() * copy.length);
      const emoji = copy[index];

      copy.splice(index, 1);
      pairs.push(emoji);
    }
    pairs.push(...pairs);

    return pairs;
  }
</script>

<div class="game">
  <div class="info" />
  <div class="grid-container">
    <Grid {grid}/>
  </div>

  <div class="info" />
</div>

<style>
  .game {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100%;
    font-size: min(1vmin, 0.5rem);
  }

  .info {
    width: 80em;
    height: 10em;
    background: purple;
  }

  .grid-container {
    width: 80em;
    height: 80em;
    background: teal;
  }
</style>
