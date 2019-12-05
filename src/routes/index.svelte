<script>
  import Gravatar from '../../component/Gravatar.svelte';
  let size = 50;
  let email = 'notgravatar@gmail.com';
  let def = 'retro';
  let rating = 'g';
</script>

<style>
  div {
    display: flex;
    flex-direction: column;
  }

  span {
    display: block;
  }

  label {
    margin: 10px 0;
  }

  pre {
    border: 1px solid black;
    background: rgba(0, 0, 0, 0.2);
    padding: 10px;
    border-radius: 10px;
    margin: 20px 0;
  }
</style>

<svelte:head>
  <title>svelte-gravatar Playground</title>
</svelte:head>

<div>
  <h1>Options from <a href="https://en.gravatar.com/site/implement/images/" target="_blank">gravatar docs</a></h1>
  <label><span>Email:</span> <input bind:value={email}></label>
  <label><span>Size:</span> <input type=range bind:value={size} min="20" max="500"></label>
  <label>
    <span>Default: </span>
    <select bind:value={def}>
      <option value="404">404</option>
      <option value="mp">mp (mysterious-person)</option>
      <option value="identicon">identicon</option>
      <option value="monsterid">monsterid</option>
      <option value="wavatar">wavatar</option>
      <option value="retro">retro</option>
      <option value="robohash">robohash</option>
      <option value="blank">blank</option>
    </select>
  </label>
  <label>
    <span>Rating: </span>
    <select bind:value={rating}>
      <option value="g">g</option>
      <option value="pg">pg</option>
      <option value="r">r</option>
      <option value="x">x</option>
    </select>
  </label>
  <Gravatar {email} {size} default={def} {rating} />

  <pre>
{`<script>
  import Gravatar from 'svelte-gravatar';
</script>`}

{`<Gravatar email="${email}" size="{${size}}" default="${def}" rating="${rating}" />`}
  </pre>
</div>
