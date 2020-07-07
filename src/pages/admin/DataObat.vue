<template>
  <q-page padding>
    <div class="row q-mb-md col-gutter-md">
      <div class="col-md-12 col-xs-12 col-lg-12">
        <div class="row">
          <div class="col-auto">
            <div class="left blue"></div>
          </div>
          <div class="col">
            <q-banner inline-actions class="text-blue-grey-14">
              <div class="text-h6">Data Obat</div>
              <div>Data Obat Apotik Sederhana</div>
            </q-banner>
          </div>
        </div>
      </div>
    </div>
    <q-card flat>
        <q-table
          :data="data"
          flat
          :columns="columns"
          row-key="name"
        >
          <template v-slot:body="props">
            <q-tr :props="props">
              <q-td key="namaObat" :props="props">
                {{ props.row.namaObat }}
              </q-td>
              <q-td key="harga" :props="props">
                {{ props.row.harga }}
              </q-td>
              <q-td key="tahun" :props="props">
                {{ props.row.tahun }}
              </q-td>
              <q-td key="golongan" :props="props">
                {{ props.row.golongan }}
              </q-td>
              <q-td key="deskripsi" :props="props">
                <div class="ellipsis" style="max-widht: 200px;">
                    {{ props.row.deskripsi }}
                </div>
              </q-td>
              <q-td key="gambar" :props="props">
                <q-img
                :src="`${$baseImageURL}/${props.row.image}`"
                spinner-color="white"
                />
              </q-td>
              <q-td key="aksi" :props="props">
                <div class="row q-gutter-md">
                    <q-btn :to="{ name: 'formEditObat', params: { id: props.row._id } }" label="Edit" icon="edit" color="warning" unelevated/>
                    <q-btn @click="deleteObat(props.row._id)" label="Hapus" icon="delete" color="negative" unelevated/>
                </div>
              </q-td>
            </q-tr>
          </template>
        </q-table>
    </q-card>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      columns: [
        { name: 'namaObat', align: 'left', label: 'Nama Obat', field: 'namaObat', sortable: true },
        { name: 'harga', align: 'left', label: 'Harga', field: 'harga', sortable: true },
        { name: 'tahun', align: 'left', label: 'Tahun', field: 'tahun', sortable: true },
        { name: 'golongan', align: 'left', label: 'Golongan', field: 'golongan', sortable: true },
        { name: 'deskripsi', align: 'left', label: 'Deskripsi', field: 'deskripsi', sortable: true },
        { name: 'gambar', align: 'left', label: 'Gambar', field: 'gambar' },
        { name: 'aksi', align: 'left', label: 'Aksi', field: 'aksi' }
      ],
      data: []
    }
  },
  created () {
    this.getData()
  },
  methods: {
    getData () {
      this.$axios.get('obat/getall')
        .then((res) => {
          if (res.data.sukses) {
            this.data = res.data.data
          } else {
            this.showNotif(res.data.pesan, 'negative')
          }
        })
    },
    deleteObat (id) {
      this.$q.dialog({
        title: 'Konfirmasi',
        message: 'Apakah Anda Yakin',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.$axios.delete(`obat/delete/${id}`)
          .then(res => {
            if (res.data.sukses) {
              this.$showNotif(res.data.pesan, 'positive')
              this.getData()
            } else {
              this.$showNotif(res.data.pesan, 'negative')
            }
          })
      })
    }
  }
}
</script>
<style scoped>
  .left {
    width: 5px;
    height: 100%;
    background: aqua;
  }
</style>
