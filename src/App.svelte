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
  function edit(id) {
    //order list but get id first
    document.getElementById('formedit').style.display = 'block';
    document.getElementById('formadd').style.display = 'none';
    document.getElementById('id').value = id;
    //find index of id in list
    var index = list.findIndex(x => x.id == id);
    //move list[index] to list[0]
    //var temp = list[index];
    //add temp to front of list
    //list.unshift(temp);
    //remove temp from list
    //list.splice(index + 1, 1);
    console.log(index);
    document.getElementById('editname').value = list[index].name;
    document.getElementById('editnickname').value = list[index].nickname;
    document.getElementById('editaddress').value = list[index].address;
  }
  function onlynotprinted() {
    list = list.filter(x => x.printed == 0);
  }
  function add() {
    document.getElementById('formedit').style.display = 'none';
    document.getElementById('formadd').style.display = 'block';
  }
</script>

<svelte:head>
	<title>Hello world</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.0/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-gH2yIJqKdNHPEq0n4Mqa/HGKIhSkIHeL5AyhkYV8i59U5AR6csBvApHHNl/vI1Bx" crossorigin="anonymous">
</svelte:head>

<main>
  <form action="https://mkrm.pwisetthon.com/list_edit.php" method="post" id="formedit" style="display: none;">
    <input type="hidden" name="id" id="id" value="">
    <input type="text" name="name" id="editname" placeholder="ชื่อ" class="form-control">
    <input type="text" name="nickname" id="editnickname" placeholder="ชื่อเล่น" class="form-control">
    <input type="text" name="address" id="editaddress" placeholder="ที่อยู่" class="form-control">
    <input type="submit" value="Add" class="btn btn-primary">
  </form>
  <button on:click={() => onlynotprinted()} class="btn btn-primary">แสดงเฉพาะที่ยังไม่ปริ้น</button>
  <table class="table">
    <thead>
      <tr>
        <th>ชื่อ</th>
        <th>ชื่อเล่น</th>
        <th>ที่อยู่</th>
        <th>สถานะการปริ้น</th>
        <th>แก้ไข</th>
      </tr>
    </thead>
    <tbody>
    {#each list as player}
      <tr>
        <td>{player.name}</td>
        <td>{player.nickname}</td>
        <td>{player.address}</td>
        <td>{#if player.printed == 0}❌{:else}✅{/if}</td>
        <td>
          <button class="btn btn-primary" on:click={() => edit(player.id)}>แก้ไข</button>
        </td>
      </tr>
    {/each}
    </tbody>
  </table>
  <button on:click={() => add()} class="btn btn-primary">เพิ่ม</button>
  <form action="https://mkrm.pwisetthon.com/list_add.php" method="post" id="formadd" style="display: none;">
    <input type="text" name="name" placeholder="Name" class="form-control">
    <input type="text" name="nickname" placeholder="Nickname" class="form-control">
    <input type="text" name="address" placeholder="Address" class="form-control">
    <input type="submit" value="Add" class="btn btn-primary">
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
