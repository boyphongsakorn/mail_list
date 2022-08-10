<script>
  //import svelteLogo from './assets/svelte.svg'
  //import Counter from './lib/Counter.svelte'
  //get json from mkrm.pwisetthon.com
  var list = [];
  (async () => {
    const response = await fetch('https://anywhere.pwisetthon.com/https://mkrm.pwisetthon.com/list_show.php');
    const data = await response.json();
    console.log(data);
    list = data;
  })();
</script>

<svelte:head>
	<title>Hello world</title>
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
</svelte:head>

<main>
  <table>
    <tr>
      <th>ชื่อ</th>
      <th>ชื่อเล่น</th>
      <th>ที่อยู่</th>
    </tr>
    {#each list as player}
      <tr>
        <td>{player.name}</td>
        <td>{player.nickname}</td>
        <td>{player.address}</td>
      </tr>
    {/each}
  </table>
  เพิ่มรายชื่อ
  <form action="https://mkrm.pwisetthon.com/list_add.php" method="post">
    <input type="text" name="name" placeholder="Name">
    <input type="text" name="nickname" placeholder="Nickname">
    <input type="text" name="address" placeholder="Address">
    <input type="submit" value="Add">
  </form>
</main>

<style>
  table {
    border-collapse: collapse;
    border: 1px solid #ccc;
  }
  tr {
    border-collapse: collapse;
    border: 1px solid #ccc;
  }
  th {
    border-collapse: collapse;
    border: 1px solid #ccc;
    padding: 5px;
  }
  td {
    border-collapse: collapse;
    border: 1px solid #ccc;
    padding: 5px;
  }
</style>
