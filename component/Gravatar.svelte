<script>
  import getMD5 from 'md5';
  import Waypoint from 'svelte-waypoint';
  import Empty from './Empty.svelte';

  export let size = 50;
  export let alt = undefined;
  export let rating = 'g';
  export let md5 = '';
  export let protocol = '//';
  export let email;
  export let useWaypoint = true;
  export let waypointOptions = {};
  export let domain = 'en.gravatar.com';

  let hasSrcset = typeof window === 'undefined' ? true : 'srcset' in document.createElement('img');

  $: formattedEmail = (email || '').trim().toLowerCase()
  $: def = $$props.default || 'retro';
  $: extraClass = $$props.class || '';
  $: extraStyles = $$props.style || '';
  $: base = `${protocol}${domain}/avatar/`;
  $: queryString = getQuery(size, rating, def, 1);
  $: retinaQuerystring = getQuery(size, rating, def, 2);
  $: hash = md5 || getMD5(formattedEmail, {encoding: 'binary'});
  $: src = `${base}${hash}?${queryString}`;
  $: retinaSrc = `${base}${hash}?${retinaQuerystring}`;
  $: formattedSize = typeof size === 'number' ? `${size}px` : size;
  $: WrapperComponent = useWaypoint ? Waypoint : Empty;

  function getQuery(s, r, d, m) {
    return `s=${s*m}&r=${r}&d=${d}`;
  }

  function isRetina() {
    if (typeof window !== "undefined" && !!window) {
      let mediaQuery = "(-webkit-min-device-pixel-ratio: 1.25), (min--moz-device-pixel-ratio: 1.25), (-o-min-device-pixel-ratio: 5/4), (min-resolution: 1.25dppx)";
      if (window.devicePixelRatio > 1.25) {
        return true;
      }
      if (window.matchMedia && window.matchMedia(mediaQuery).matches) {
        return true;
      }
    }
    return false;
  }
</script>

<WrapperComponent {...waypointOptions}>
  <img
    alt="{typeof alt === undefined ? `Gravatar for ${formattedEmail}` : alt}"
    style="{extraStyles}"
    class="{extraClass}"
    src="{isRetina() && !hasSrcset ? retinaSrc : src}"
    srcset="{hasSrcset ? `${retinaSrc} 2x` : undefined}"
    width="{formattedSize}"
    height="{formattedSize}"
    on:error
  />
</WrapperComponent>
