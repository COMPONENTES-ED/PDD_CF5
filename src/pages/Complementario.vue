<template>
  <div class="curso-main-container complementario">
    <BannerInterno
      icono="far fa-folder-open"
      titulo="Material complementario"
    ></BannerInterno>
    <div class="container tarjeta tarjeta--blanca p-4 p-md-5 mb-5">
      <div class="table-responsive">
        <table>
          <thead>
            <tr>
              <th colspan="3" scope="col">Tema</th>
              <th colspan="5" scope="col">Referencia APA del material</th>
              <th colspan="2" scope="col">Tipo</th>
              <th colspan="2" scope="col">Enlace</th>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="(item, index) in computedData"
              :key="'complementario-' + index"
            >
              <td
                class="text-start"
                colspan="3"
                scope="row"
                v-html="item.tema"
              ></td>
              <td
                class="text-start"
                colspan="5"
                scope="row"
                v-html="item.referencia"
              ></td>
              <td colspan="2" v-html="item.tipo"></td>
              <td colspan="2">
                <div class="complementario__enlaces">
                  <a
                    v-for="(link, linkIndex) of item.link"
                    :key="linkIndex"
                    class="complementario__btn"
                    :href="link"
                    target="_blank"
                    ><i class="fas fa-external-link-alt"></i
                  ></a>
                </div>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'MaterialComplementario',
  computed: {
    complementarioData() {
      return [
        {
          tema: 'El algoritmo ideal',
          referencia:
            'Ecosistema de Recursos Educativos Digitales SENA. (2023c, octubre 10). El algoritmo ideal.',
          tipo: 'Video',
          link: 'https://www.youtube.com/watch?v=ZgkwSKyGpnY',
        },
        {
          tema: '¿Qué es <i>Machine learning</i>?',
          referencia:
            'Ecosistema de Recursos Educativos Digitales SENA. (2020, 13 septiembre). ¿Qué es Machine learning?',
          tipo: 'Video',
          link: 'https://www.youtube.com/watch?v=J9w6KquPKbE',
        },
        {
          tema: 'Introducción al <i>Machine learning</i>',
          referencia:
            'Ecosistema de Recursos Educativos Digitales SENA. (2023a, septiembre 15). Introducción al <i>machine learning.</i>',
          tipo: 'Video',
          link: 'https://www.youtube.com/watch?v=xwjQmGJ3q0I',
        },
        {
          tema: '<i>Machine learning</i> con Python',
          referencia:
            'Ecosistema de Recursos Educativos Digitales SENA. (2023c, octubre 10). Machine learning con Python.',
          tipo: 'Video',
          link: 'https://www.youtube.com/watch?v=noMy4-zjR9Q',
        },
        {
          tema: 'Modelos y metodologías de analítica',
          referencia:
            'Ecosistema de Recursos Educativos Digitales SENA. (2023e, marzo 27). Modelos y metodologías de analítica.',
          tipo: 'Video',
          link: 'https://www.youtube.com/watch?v=96pohadjEWE ',
        },
        {
          tema: 'Análisis exploratorio de datos',
          referencia:
            'Limpiar datos de Excel, CSV, PDF y Hojas de cálculo de Google con el intérprete de datos. (s. f.). Tableau.',
          tipo: 'Portal web',
          link:
            'https://help.tableau.com/current/pro/desktop/es-es/data_interpreter.htm ',
        },
        {
          tema: 'Definición de pandas',
          referencia:
            'Ecosistema de Recursos Educativos Digitales SENA. (2023b, septiembre 20). Definición de pandas.',
          tipo: 'Video',
          link: 'https://www.youtube.com/watch?v=W48LYsToQHQ',
        },
      ]
    },
    computedData() {
      const data = this.complementarioData
      return data.map(item => {
        let nuevoLink = []
        if (item.link) {
          if (typeof item.link === 'string') {
            nuevoLink.push(item.link)
          } else {
            nuevoLink = item.link
          }
        } else if (item.descarga) {
          if (typeof item.descarga === 'string') {
            nuevoLink.push(this.obtenerLink(item.descarga))
          } else {
            item.descarga.forEach(link => {
              nuevoLink.push(this.obtenerLink(link))
            })
          }
        }
        return {
          ...item,
          link: nuevoLink,
        }
      })
    },
  },
}
</script>

<style lang="sass">
.complementario
  &__enlaces
    display: flex
    justify-content: center
    flex-wrap: wrap
    a
      margin: 0 5px
  &__btn
    font-size: 1.5em
    line-height: 1em
table
  width: calc(100% - 1px)
  min-width: 800px
  thead
    background-color: $color-sistema-e
    th
      border-color: $color-sistema-e
  th, td
    padding: 25px 20px
    text-align: center
</style>
