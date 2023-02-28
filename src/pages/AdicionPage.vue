<template>
  <div>
    <h1>Adici&oacute;n de Materias</h1>
  </div>
  <div class="q-pa-lg">
    <div class="row">
      <div class="col-12 col-md-4">
        <h6>Materias Ofertadas</h6>
        <div class="q-py-sm q-pr-lg" style="">
          <q-scroll-area style="height: 400px; border: 2px;">
            <div v-for="(materia, materiaIndex) in materias" :key="materiaIndex">
              <q-expansion-item dense class="overflow-hidden"
                style="border-radius: 20px; margin-bottom: 10px; margin-right: 15px;"
                :label="`${materia.nombre} - ${materia.sigla}`" header-class="bg-amber-2 text-black text-bold"
                header-style="font-size: 15px; height: 40px;" expand-icon-class="text-black" default-opened>
                <q-card class="text-courrier">
                  <q-card-section>
                    <div style="margin-top: -20px;">
                      <table class="full-width" style="background: transparent;">
                        <thead style="font-size: 11px;">
                          <tr>
                            <th style="width: 20px;">Grupo</th>
                            <th>Docente</th>
                            <th style="width: 20px;">Cupo</th>
                            <th>Horario</th>
                          </tr>
                        </thead>
                      </table>
                    </div>
                    <div v-for="(grupo, grupoIndex) in materia.grupos" :key="grupoIndex" @click="handleGroupClick(grupo)"
                      style="margin-left: -10px; margin-right: -10px;">

                      <q-card style="border-radius: 20px; height: 50px; margin-bottom: 10px;"
                        :class="{ 'selected': gruposSelect.includes(grupo) }" flat bordered>
                        <q-card-section style="padding: 0px 10px;">
                          <div style="justify-items: center; align-items: center; display: flex;">
                            <span style="margin: 0 10px; width: 25px; text-align: center;"><strong>{{ grupo.nombre
                            }}</strong></span>

                            <span style="margin-left: 20px; width: 100px; text-align: center; overflow-x: auto;">{{
                              grupo.docente }}</span>

                            <span style="margin-left: 10px; width: 25px; text-align: center;">{{ grupo.cupos }}</span>

                            <div style="display: block;">
                              <span v-for="(horario, horarioIndex) in grupo.horarios" :key="horarioIndex"
                                style="margin-left: 10px; font-size: 11px; width: 150px; text-align: center; display: block">
                                {{ horario.dia }} {{ horario.hora_inicio }} - {{ horario.hora_fin }}
                              </span>
                            </div>
                          </div>
                        </q-card-section>
                      </q-card>

                    </div>
                  </q-card-section>
                </q-card>
              </q-expansion-item>
            </div>
          </q-scroll-area>
          <q-btn style="background-color: #FFECA7;" icon="save" label="Grabar materias"
            class="full-width q-my-md q-py-sm text-black font-bold" />
        </div>

      </div>
      <div class="col-12 col-md-8 container">
        <h6>Horarios</h6>
        <table>
          <thead>
            <tr class="table-header">
              <th class="border-left"></th>
              <th>Lunes</th>
              <th>Martes</th>
              <th>Mi&eacute;rcoles</th>
              <th>Jueves</th>
              <th class="border-right">Viernes</th>
            </tr>
          </thead>
          <tbody style="text-align: center;">
            <tr v-for="(row, rowIndex) in rows" :key="rowIndex">
              <td v-for="(cell, cellIndex) in row" :key="cellIndex" :style="cell.style" :rowspan="cell.rowspan"
                :colspan="cell.colspan">
                <template v-if="cell.horario">
                  {{ cell.value }}
                </template>
                <template v-else>
                  <strong>{{ cell.materia }} </strong> <br> {{ cell.docente }} <br> <strong>{{ cell.grupo }}</strong>
                </template>
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
  data() {

    var gruposSelect = [];
    var indexGrupoCell = [];

    var colores = [
      '#ffe4e1',
      '#d8f8e1',
      '#fcb7af',
      '#b0f2c2',
      '#b0c2f2',
      '#fabfb7',
      '#fdf9c4',
      '#ffda9e',
      '#c5c6c8',
      '#b2e2f2',
      '#a3ffac',
    ];

    var materias = [
      {// Calculo 1
        nombre: 'Cálculo 1',
        sigla: 'MAT101',
        semestre: 1,
        creditos: 4,
        grupos: [
          {// Grupo SC
            nombre: 'SC',
            docente: 'Ing. Mario Lopez',
            materia: 'Calculo 1',
            cupos: 24,
            codigo: 'MAT101-SC',
            horarios: [
              {// Lunes
                dia: 'Lun',
                hora_inicio: '10:00',
                hora_fin: '11:30',
              },
              {// Miercoles
                dia: 'Mie',
                hora_inicio: '10:00',
                hora_fin: '11:30',
              },
              {// Viernes
                dia: 'Vie',
                hora_inicio: '10:00',
                hora_fin: '11:30',
              },
            ]
          },
          {// Grupo Z1
            nombre: 'Z1',
            docente: 'Ing. Katime Esther',
            materia: 'Calculo 1',
            cupos: 4,
            codigo: 'MAT101-Z1',
            horarios: [
              {// Martes
                dia: 'Mar',
                hora_inicio: '10:00',
                hora_fin: '11:30',
              },
              {// Jueves
                dia: 'Jue',
                hora_inicio: '10:00',
                hora_fin: '11:30',
              },
            ]
          }
        ]
      },
      {// Fisica 1
        nombre: 'Física 1',
        sigla: 'FIS100',
        semestre: 1,
        creditos: 5,
        grupos: [
          {
            nombre: 'Z1',
            docente: 'Ing. Marcos Zeballos',
            materia: 'Fisica 1',
            cupos: 16,
            codigo: 'FIS100-Z1',
            horarios: [
              {
                dia: 'Mar',
                hora_inicio: '07:00',
                hora_fin: '09:15',
              },
              {
                dia: 'Jue',
                hora_inicio: '07:00',
                hora_fin: '09:15',
              },
              {
                dia: 'Lun',
                hora_inicio: '13:00',
                hora_fin: '14:30',
              }
            ]
          },
          {
            nombre: 'Z2',
            docente: 'Ing. Mario Sanchez',
            materia: 'Fisica 1',
            cupos: 16,
            codigo: 'FIS100-Z2',
            horarios: [
              {// Lunes
                dia: 'Lun',
                hora_inicio: '10:00',
                hora_fin: '11:30',
              },
              {// Miercoles
                dia: 'Mie',
                hora_inicio: '10:00',
                hora_fin: '11:30',
              },
              {// Viernes
                dia: 'Vie',
                hora_inicio: '10:00',
                hora_fin: '11:30',
              },
            ]
          }
        ]
      }
    ]

    // const rows = [
    //   [
    //     {
    //       value: '07:00 - 07:45',
    //       codigo_inicio: 700,
    //       codigo_fin: 745,
    //       horario: true,
    //     },
    //     {
    //       codigo: 'lunes',
    //       value: '-',
    //     },
    //     {
    //       codigo: 'martes',
    //       value: '-',
    //     },
    //     {
    //       codigo: 'miercoles',
    //       value: '-'
    //     },
    //     {
    //       codigo: 'jueves',
    //       value: '-',
    //     },
    //     {
    //       codigo: 'viernes',
    //       value: '-'
    //     },
    //   ],
    //   [
    //     {
    //       value: '07:45 - 08:30',
    //       codigo_inicio: 745,
    //       codigo_fin: 830,
    //       horario: true,
    //     },
    //     {
    //       codigo: 'lunes',
    //       value: '-',
    //     },
    //     {
    //       codigo: 'martes',
    //       value: '-',
    //     },
    //     {
    //       codigo: 'miercoles',
    //       value: '-'
    //     },
    //     {
    //       codigo: 'jueves',
    //       value: '-',
    //     },
    //     {
    //       codigo: 'viernes',
    //       value: '-'
    //     },
    //   ],
    //   [
    //     {
    //       value: '08:30 - 09:15',
    //       codigo_inicio: 830,
    //       codigo_fin: 915,
    //       horario: true,
    //     },
    //     {
    //       codigo: 'lunes',
    //       value: '-',
    //     },
    //     {
    //       codigo: 'martes',
    //       value: '-',
    //     },
    //     {
    //       codigo: 'miercoles',
    //       value: '-',
    //     },
    //     {
    //       codigo: 'jueves',
    //       value: '-',
    //     },
    //     {
    //       codigo: 'viernes',
    //       value: '-',
    //     },
    //   ],
    //   [
    //     {
    //       value: '09:15 - 10:00',
    //       codigo_inicio: 915,
    //       codigo_fin: 1000,
    //       horario: true,
    //     },
    //     {
    //       codigo: 'lunes',
    //       value: '-',
    //     },
    //     {
    //       codigo: 'martes',
    //       value: '-',
    //     },
    //     {
    //       codigo: 'miercoles',
    //       value: '-',
    //     },
    //     {
    //       codigo: 'jueves',
    //       value: '-'
    //     },
    //     {
    //       codigo: 'viernes',
    //       value: '-',
    //     },
    //   ],
    //   [
    //     {
    //       value: '10:00 - 10:45',
    //       codigo_inicio: 1000,
    //       codigo_fin: 1045,
    //       horario: true,
    //     },
    //     {
    //       codigo: 'lunes',
    //       value: '-'
    //     },
    //     {
    //       codigo: 'martes',
    //       value: '-'
    //     },
    //     {
    //       codigo: 'miercoles',
    //       value: '-'
    //     },
    //     {
    //       codigo: 'jueves',
    //       value: '-'
    //     },
    //     {
    //       codigo: 'viernes',
    //       value: '-'
    //     },
    //   ],
    //   [
    //     {
    //       value: '10:45 - 11:30',
    //       codigo_inicio: 1045,
    //       codigo_fin: 1130,
    //       horario: true,
    //     },
    //     {
    //       codigo: 'lunes',
    //       value: '-'
    //     },
    //     {
    //       codigo: 'martes',
    //       value: '-'
    //     },
    //     {
    //       codigo: 'miercoles',
    //       value: '-'
    //     },
    //     {
    //       codigo: 'jueves',
    //       value: '-'
    //     },
    //     {
    //       codigo: 'viernes',
    //       value: '-'
    //     },
    //   ],
    //   [
    //     {
    //       value: '11:30 - 12:15',
    //       codigo_inicio: 1130,
    //       codigo_fin: 1215,
    //       horario: true,
    //     },
    //     {
    //       codigo: 'lunes',
    //       value: '-'
    //     },
    //     {
    //       codigo: 'martes',
    //       value: '-'
    //     },
    //     {
    //       codigo: 'miercoles',
    //       value: '-'
    //     },
    //     {
    //       codigo: 'jueves',
    //       value: '-'
    //     },
    //     {
    //       codigo: 'viernes',
    //       value: '-'
    //     },
    //   ],
    //   [
    //     {
    //       value: '12:15 - 13:00',
    //       codigo_inicio: 1215,
    //       codigo_fin: 1300,
    //       horario: true,
    //     },
    //     {
    //       codigo: 'lunes',
    //       value: '-'
    //     },
    //     {
    //       codigo: 'martes',
    //       value: '-'
    //     },
    //     {
    //       codigo: 'miercoles',
    //       value: '-'
    //     },
    //     {
    //       codigo: 'jueves',
    //       value: '-'
    //     },
    //     {
    //       codigo: 'viernes',
    //       value: '-'
    //     },
    //   ],
    //   [
    //     {
    //       value: '13:00 - 13:45',
    //       codigo_inicio: 1300,
    //       codigo_fin: 1345,
    //       horario: true,
    //     },
    //     {
    //       codigo: 'lunes',
    //       value: '-'
    //     },
    //     {
    //       codigo: 'martes',
    //       value: '-'
    //     },
    //     {
    //       codigo: 'miercoles',
    //       value: '-'
    //     },
    //     {
    //       codigo: 'jueves',
    //       value: '-'
    //     },
    //     {
    //       codigo: 'viernes',
    //       value: '-'
    //     },
    //   ],
    //   [
    //     {
    //       value: '13:45 - 14:30',
    //       codigo_inicio: 1345,
    //       codigo_fin: 1430,
    //       horario: true,
    //     },
    //     {
    //       codigo: 'lunes',
    //       value: '-'
    //     },
    //     {
    //       codigo: 'martes',
    //       value: '-'
    //     },
    //     {
    //       codigo: 'miercoles',
    //       value: '-'
    //     },
    //     {
    //       codigo: 'jueves',
    //       value: '-'
    //     },
    //     {
    //       codigo: 'viernes',
    //       value: '-'
    //     },
    //   ],
    // ]

    const rows = [
      [
        {
          value: '07:00 - 07:45',
          codigo_inicio: 700,
          codigo_fin: 745,
          horario: true,
        },
        {
          codigo: 'lunes',
          value: '-',
        },
        {
          codigo: 'martes',
          materia: 'Fisica 1',
          docente: 'Ing. Juan Perez',
          grupo: 'Z1',
          style: 'background-color: #CBECFF; border-radius: 20px; font-size: 12px;',
          rowspan: 3,
        },
        {
          codigo: 'miercoles',
          value: '-'
        },
        {
          codigo: 'jueves',
          materia: 'Fisica 1',
          docente: 'Ing. Juan Perez',
          grupo: 'Z1',
          style: 'background-color: #CBECFF; border-radius: 20px; font-size: 12px;',
          rowspan: 3,
        },
        {
          codigo: 'viernes',
          value: '-'
        },
      ],
      [
        {
          value: '07:45 - 08:30',
          codigo_inicio: 745,
          codigo_fin: 830,
          horario: true,
        },
        {
          codigo: 'lunes',
          value: '-',
        },
        {
          codigo: 'martes',
          materia: 'Fisica 1',
          docente: 'Ing. Juan Perez',
          grupo: 'Z1',
          style: 'display: none;',
        },
        {
          codigo: 'miercoles', value: '-'
        },
        {
          codigo: 'jueves',
          materia: 'Fisica 1',
          docente: 'Ing. Juan Perez',
          grupo: 'Z1',
          style: 'display: none;',
        },
        {
          codigo: 'viernes', value: '-'
        },
      ],
      [
        {
          value: '08:30 - 09:15',
          codigo_inicio: 830,
          codigo_fin: 915,
          horario: true,
        },
        {
          codigo: 'lunes',
          materia: 'Calculo 1',
          docente: 'Ing. Sanchez Mario',
          grupo: 'SC',
          style: 'background-color: #FFCBCB; border-radius: 20px; font-size: 12px;',
          rowspan: 2,
        },
        {
          codigo: 'martes',
          materia: 'Fisica 1',
          docente: 'Ing. Juan Perez',
          grupo: 'Z1',
          style: 'display: none;',
        },
        {
          codigo: 'miercoles',
          materia: 'Calculo 1',
          docente: 'Ing. Sanchez Mario',
          grupo: 'SC',
          style: 'background-color: #FFCBCB; border-radius: 20px; font-size: 12px;',
          rowspan: 2,
        },
        {
          codigo: 'jueves',
          materia: 'Fisica 1',
          docente: 'Ing. Juan Perez',
          grupo: 'Z1',
          style: 'display: none;',
        },
        {
          codigo: 'viernes',
          materia: 'Calculo 1',
          docente: 'Ing. Sanchez Mario',
          grupo: 'SC',
          style: 'background-color: #FFCBCB; border-radius: 20px; font-size: 12px;',
          rowspan: 2,
        },
      ],
      [
        {
          value: '09:15 - 10:00',
          codigo_inicio: 915,
          codigo_fin: 1000,
          horario: true,
        },
        {
          codigo: 'lunes',
          materia: 'Calculo 1',
          docente: 'Ing. Sanchez Mario',
          grupo: 'SC',
          style: 'display: none;',
        },
        {
          codigo: 'martes',
          value: '-',
        },
        {
          codigo: 'miercoles',
          materia: 'Calculo 1',
          docente: 'Ing. Sanchez Mario',
          grupo: 'SC',
          style: 'display: none;',
        },
        {
          codigo: 'jueves', value: '-'
        },
        {
          codigo: 'viernes',
          materia: 'Calculo 1',
          docente: 'Ing. Sanchez Mario',
          grupo: 'SC',
          style: 'display: none;',
        },
      ],
      [
        {
          value: '10:00 - 10:45',
          codigo_inicio: 1000,
          codigo_fin: 1045,
          horario: true,
        },
        {
          codigo: 'lunes', value: '-'
        },
        {
          codigo: 'martes', value: '-'
        },
        {
          codigo: 'miercoles', value: '-'
        },
        {
          codigo: 'jueves', value: '-'
        },
        {
          codigo: 'viernes', value: '-'
        },
      ],
      [
        {
          value: '10:45 - 11:30',
          codigo_inicio: 1045,
          codigo_fin: 1130,
          horario: true,
        },
        {
          codigo: 'lunes', value: '-'
        },
        {
          codigo: 'martes', value: '-'
        },
        {
          codigo: 'miercoles', value: '-'
        },
        {
          codigo: 'jueves', value: '-'
        },
        {
          codigo: 'viernes', value: '-'
        },
      ],
      [
        {
          value: '11:30 - 12:15',
          codigo_inicio: 1130,
          codigo_fin: 1215,
          horario: true,
        },
        {
          codigo: 'lunes', value: '-'
        },
        {
          codigo: 'martes', value: '-'
        },
        {
          codigo: 'miercoles', value: '-'
        },
        {
          codigo: 'jueves', value: '-'
        },
        {
          codigo: 'viernes', value: '-'
        },
      ],
      [
        {
          value: '12:15 - 13:00',
          codigo_inicio: 1215,
          codigo_fin: 1300,
          horario: true,
        },
        {
          codigo: 'lunes', value: '-'
        },
        {
          codigo: 'martes', value: '-'
        },
        {
          codigo: 'miercoles', value: '-'
        },
        {
          codigo: 'jueves', value: '-'
        },
        {
          codigo: 'viernes', value: '-'
        },
      ],
      [
        {
          value: '13:00 - 13:45',
          codigo_inicio: 1300,
          codigo_fin: 1345,
          horario: true,
        },
        {
          codigo: 'lunes', value: '-'
        },
        {
          codigo: 'martes', value: '-'
        },
        {
          codigo: 'miercoles', value: '-'
        },
        {
          codigo: 'jueves', value: '-'
        },
        {
          codigo: 'viernes', value: '-'
        },
      ],
      [
        {
          value: '13:45 - 14:30',
          codigo_inicio: 1345,
          codigo_fin: 1430,
          horario: true,
        },
        {
          codigo: 'lunes', value: '-'
        },
        {
          codigo: 'martes', value: '-'
        },
        {
          codigo: 'miercoles', value: '-'
        },
        {
          codigo: 'jueves', value: '-'
        },
        {
          codigo: 'viernes', value: '-'
        },
      ],
    ]

    return {
      materias,
      indexGrupoCell,
      colores,
      gruposSelect,
      rows,
    };
  },
  methods: {
    toggleButton(index) {
      console.log(index);
      this.isSelected = !this.isSelected
    },
    handleGroupClick(grupo) {
      if (this.gruposSelect.includes(grupo)) {
        this.eliminarGrupo(grupo)
        this.delGrupoHorario(grupo.codigo);
      } else {
        var materiaExiste = this.existeMateria(grupo.materia);
        //console.log(materiaExiste);
        if (materiaExiste != -1)
          this.eliminarGrupo(materiaExiste);

        this.gruposSelect.push(grupo);
        this.addGrupoHorario(grupo)
      }
      console.log(this.gruposSelect);
    },
    existeMateria(materia) {
      for (let index = 0; index < this.gruposSelect.length; index++) {
        const grupo = this.gruposSelect[index]
        if (grupo.materia == materia)
          return grupo
      }

      return -1
    },
    eliminarGrupo(grupo) {
      const index = this.gruposSelect.indexOf(grupo);
      this.gruposSelect.splice(index, 1);
    },
    addGrupoHorario(grupo) {
      const dias = [];
      const horarios = [];
      grupo.horarios.forEach(element => {
        const horario = [];
        dias.push(this.getDay(element.dia))
        horario.push(this.getHora(element.hora_inicio))
        horario.push(this.getHora(element.hora_fin))
        horarios.push(horario);
      });

      const numRandom = Math.floor(Math.random() * this.colores.length)
      const color = this.colores[numRandom];
      this.colores.splice(numRandom, 1);
      console.log(color);

      for (let index = 0; index < horarios.length; index++) {
        const cantFila = this.getCantFilas(horarios[index])

        const new_grupo = {
          codigo: `${this.getDay(dias[index])}`,
          materia: `${grupo.materia}`,
          docente: `${grupo.docente}`,
          grupo: `${grupo.nombre}`,
          style: `background-color: ${color}; border-radius: 20px; font-size: 12px;`,
          rowspan: `${cantFila}`,
        }

        const new_grupo_x = {
          codigo: `${this.getDay(dias[index])}`,
          materia: `${grupo.materia}`,
          docente: `${grupo.docente}`,
          grupo: `${grupo.nombre}`,
          style: 'display: none;',
        }

        for (let i = 0; i < this.rows.length; i++) {
          if (this.rows[i][0].codigo_inicio == horarios[index][0]) {
            for (let j = 0; j < this.rows[i].length; j++) {
              var fila = 0
              var flag = true
              if (this.rows[i][j].codigo == dias[index]) {
                while (fila < cantFila) {
                  if (flag) {
                    this.rows[i + fila][j] = new_grupo
                    flag = false
                  } else {
                    this.rows[i + fila][j] = new_grupo_x
                  }
                  fila++
                }

                this.indexGrupoCell.push(
                  {
                    codigo_grupo: `${grupo.codigo}`,
                    color: `${color}`,
                    dia: `${dias[index]}`,
                    rows: `${cantFila}`,
                    i: `${i}`,
                    j: `${j}`,
                  }
                )
              }
            }
          }

        }
      }
      //console.log(this.indexGrupoCell);
    },
    delGrupoHorario(codigo) {
      var flag = true;
      this.indexGrupoCell.forEach(element => {
        if (element.codigo_grupo == codigo) {
          var i = element.i
          var j = element.j
          var dia = element.dia
          var cantFila = element.rows

          console.log(i, j, dia, cantFila);
          this.rows[i][j] = {
            codigo: `${dia}`,
            value: '-',
          }

          if (flag)
            this.colores.push(element.color);
        }
      });
    },
    getDay(dia) {
      switch (dia) {
        case 'Lun':
          dia = 'lunes';
          break;
        case 'Mar':
          dia = 'martes';
          break;
        case 'Mie':
          dia = 'miercoles';
          break;
        case 'Jue':
          dia = 'jueves';
          break;
        case 'Vie':
          dia = 'viernes';
          break;
        default:
          dia = 'Undefined';
          break;
      }

      return dia;
    },
    getHora(hora) {
      return parseInt(hora.substring(0, 2) + hora.substring(3, hora.length));
    },
    getCantFilas(hora) {
      const totalMin = hora[1] - hora[0]
      switch (totalMin) {
        case 45:
          return 1;
        case 130:
          return 2;
        case 215:
          return 3;
        case 300:
          return 4;
        default:
          return -1
      }
    }
  }
};
</script>

<style>
table {
  width: auto;
  border-radius: 20px;
  border-collapse: collapse;
  overflow: hidden;
  background-color: rgb(250, 250, 250);
}

th,
td {
  padding: 15px;
  background-color: rgba(255, 255, 255, 0.2);
  color: black;
}

th {
  text-align: center;
}

.table-header {
  background-color: #FFECA7;
  border-radius: 20px 0 0 20px;
}

.border-left {
  border-radius: 20px 0 0 20px;
}

.border-right {
  border-radius: 0 20px 20px 0;
}

th {
  height: 20px;
  border: none;
  padding: 10px;
}


td {
  font-size: 11px;
  width: 560px;
}

h1 {
  margin-top: -10px;
  margin-bottom: 10px;
  text-align: center;
  font-size: 21px;
  font-weight: bold;
}

h6 {
  margin-top: -50px;
  margin-bottom: 10px;
}

.selected {
  background-color: #E5F3FF;

}

.text-courrier {
  font-family: 'Courier New', Courier, monospace;
  font-weight: bold;
}
</style>
