<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Tabel Harga Barang</title>
<style>
body { font-family: Arial, sans-serif; padding: 20px; background: #F4F7FA; }
h2 { color: #2B4C6F; }
table { width: 100%; border-collapse: collapse; margin-top: 20px; background-color: #FFFFFF; border-radius: 10px; overflow: hidden; box-shadow: 0px 2px 8px rgba(0,0,0,0.2); }
th, td { border: 1px solid #A3B5C7; padding: 10px; text-align: center; }
th { background: #C8D9E6; font-weight: bold; }
button { padding: 10px 15px; margin-top: 15px; margin-right: 10px; cursor: pointer; border: none; color: white; background: #2B4C6F; border-radius: 5px; }
button:hover { background: #1D3A55; }
.total-row td { font-weight: bold; background: #EAF0F6; }
input[type='number'] { width: 80px; }
input[type='text'] { width: 120px; }
</style>
</head>
<body>
<h2>Tabel Harga Barang</h2>
<table id="tabelBarang">
<thead>
<tr>
<th>Nama Barang</th>
<th>Pn</th>
<th>P0</th>
<th>Qn</th>
<th>Q0</th>
<th>Hapus</th>
</tr>
</thead>
<tbody id="table-body">
<tr>
<td><input type="text" value="Beras"></td>
<td><input type="number" class="pn" value="15500"></td>
<td><input type="number" class="p0" value="15000"></td>
<td><input type="number" class="qn" value="0.9"></td>
<td><input type="number" class="q0" value="1"></td>
<td><button onclick="hapusBaris(this)">X</button></td>
</tr>
<tr>
<td><input type="text" value="Gula"></td>
<td><input type="number" class="pn" value="15500"></td>
<td><input type="number" class="p0" value="16000"></td>
<td><input type="number" class="qn" value="2"></td>
<td><input type="number" class="q0" value="1.9"></td>
<td><button onclick="hapusBaris(this)">X</button></td>
</tr>
<tr>
<td><input type="text" value="Telur"></td>
<td><input type="number" class="pn" value="30500"></td>
<td><input type="number" class="p0" value="30000"></td>
<td><input type="number" class="qn" value="2.9"></td>
<td><input type="number" class="q0" value="3"></td>
<td><button onclick="hapusBaris(this)">X</button></td>
</tr>
<tr>
<td><input type="text" value="Minyak Goreng"></td>
<td><input type="number" class="pn" value="16500"></td>
<td><input type="number" class="p0" value="17000"></td>
<td><input type="number" class="qn" value="4"></td>
<td><input type="number" class="q0" value="3.9"></td>
<td><button onclick="hapusBaris(this)">X</button></td>
</tr>
<tr>
<td><input type="text" value="Daging Ayam"></td>
<td><input type="number" class="pn" value="35500"></td>
<td><input type="number" class="p0" value="35000"></td>
<td><input type="number" class="qn" value="4.9"></td>
<td><input type="number" class="q0" value="5"></td>
<td><button onclick="hapusBaris(this)">X</button></td>
</tr>
</tbody>
<tfoot id="tfootTotal">
<tr class="total-row">
<td>Total</td>
<td id="totalPn">0</td>
<td id="totalP0">0</td>
<td id="totalQn">0</td>
<td id="totalQ0">0</td>
<td></td>
</tr>
</tfoot>
</table>
<button onclick="tambahBaris()">Tambah Baris</button>
<button onclick="hitungTotal()">Hitung Total</button>
<button onclick="hitungIndeks()">Hitung Indeks</button>
<h2>Indeks Harga</h2>
<div id="indeksOutput" style="background:#FFFFFF; padding:15px; border-radius:8px; box-shadow:0px 2px 6px rgba(0,0,0,0.2);">
</div>
<script>
function hapusBaris(btn){ btn.parentElement.parentElement.remove(); hitungTotal(); }
function tambahBaris(){
 const tbody=document.querySelector('#tabelBarang tbody');
 const tr=document.createElement('tr');
 tr.innerHTML=`
 <td><input type='text'></td>
 <td><input type='number' class='pn'></td>
 <td><input type='number' class='p0'></td>
 <td><input type='number' class='qn'></td>
 <td><input type='number' class='q0'></td>
 <td><button onclick='hapusBaris(this)'>X</button></td>`;
 tbody.appendChild(tr);
}
function hitungTotal(){
 let totalPn=0,totalP0=0,totalQn=0,totalQ0=0;
 document.querySelectorAll('tr').forEach(row=>{
   const pn=row.querySelector('.pn');
   const p0=row.querySelector('.p0');
   const qn=row.querySelector('.qn');
   const q0=row.querySelector('.q0');
   if(pn && p0 && qn && q0){
     totalPn+=Number(pn.value)||0;
     totalP0+=Number(p0.value)||0;
     totalQn+=Number(qn.value)||0;
     totalQ0+=Number(q0.value)||0;
   }
 });
 document.getElementById('totalPn').innerText=totalPn;
 document.getElementById('totalP0').innerText=totalP0;
 document.getElementById('totalQn').innerText=totalQn.toFixed(1);
 document.getElementById('totalQ0').innerText=totalQ0.toFixed(1);
}
function hitungIndeks(){
 let totalPn=0,totalP0=0,totalQn=0,totalQ0=0;
 document.querySelectorAll('tr').forEach(row=>{
   const pn=row.querySelector('.pn');
   const p0=row.querySelector('.p0');
   const qn=row.querySelector('.qn');
   const q0=row.querySelector('.q0');
   if(pn && p0 && qn && q0){
     totalPn+=Number(pn.value)||0;
     totalP0+=Number(p0.value)||0;
     totalQn+=Number(qn.value)||0;
     totalQ0+=Number(q0.value)||0;
   }
 });
 const indeksLaspeyres=((totalPn*totalQ0)/(totalP0*totalQ0)*100).toFixed(2)+'%';
 const indeksPaasche=((totalPn*totalQn)/(totalP0*totalQn)*100).toFixed(2)+'%';
 document.getElementById('indeksOutput').innerHTML=`
 <b>Laspeyres</b><br>
 Rumus: (ΣPn × ΣQ0) / (ΣP0 × ΣQ0) × 100%<br>
 Nilai: (${totalPn} × ${totalQ0}) / (${totalP0} × ${totalQ0}) × 100% = ${indeksLaspeyres}<br>
 Link: <a href="https://youtu.be/6SN8yxOvh_4?si=tZLPEpne1MVDpJ-2" target="_blank">https://youtu.be/6SN8yxOvh_4?si=tZLPEpne1MVDpJ-2</a><br><br>
 <b>Paasche</b><br>
 Rumus: (ΣPn × ΣQn) / (ΣP0 × ΣQn) × 100%<br>
 Nilai: (${totalPn} × ${totalQn.toFixed(1)}) / (${totalP0} × ${totalQn.toFixed(1)}) × 100% = ${indeksPaasche}<br>
 Link: <a href="https://youtu.be/gh6rzF_dx4o?si=kEFT7JkekxHCWQb-" target="_blank">https://youtu.be/gh6rzF_dx4o?si=kEFT7JkekxHCWQb-</a>
 `;
}
</script>
</body>
</html>
