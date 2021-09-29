<template>
  <q-page>
    <div class="row q-pb-lg">
      <div class="col-md-3"></div>
      <div class="col-xs-12 col-md-6">
        <div class="text-center">
          <q-img src="logo_taxipropio.png"></q-img>
        </div>
        <q-list>
          <q-form @submit="onSubmit">
            <q-item class="text-justify">
              <q-item-section>
                <div class="text-h5">¡TU TAXI PROPIO AL CRÉDITO!</div>
                <br>
                Estás a un paso de obtener TU TAXI PROPIO nuevo, listo para trabajar.
                Tenemos disponible la marca Chery modelo Arizzo, desde 699 dólares de inicial.
                <br>
                <br>
                ¿Qué esperas? Aprovecha que tenemos pocas unidades disponibles.
                Déjanos tus datos para pre evaluarte y ponernos en contacto contigo ;)
              </q-item-section>
            </q-item>
            <q-item class="text-center">
              <q-item-section>
                <q-input
                  autofocus
                  outlined
                  lazy-rules
                  :rules="[
                    val => (val && val.length > 0) || 'Campo obligatorio'
                  ]"
                  stack-label
                  dense
                  v-model="apellido_paterno"
                  ref="apellido_paterno"
                  label="Apellido Paterno"
                ></q-input>
              </q-item-section>
              <q-item-section>
                <q-input
                  outlined
                  lazy-rules
                  :rules="[
                    val => (val && val.length > 0) || 'Campo obligatorio'
                  ]"
                  stack-label
                  dense
                  v-model="apellido_materno"
                  ref="apellido_materno"
                  label="Apellido Materno"
                ></q-input>
              </q-item-section>
            </q-item>
            <q-item class="text-center">
              <q-item-section>
                <q-input
                  outlined
                  lazy-rules
                  :rules="[
                    val => (val && val.length > 0) || 'Campo obligatorio'
                  ]"
                  stack-label
                  dense
                  v-model="nombres"
                  ref="nombres"
                  label="Nombres"
                ></q-input>
              </q-item-section>
            </q-item>
            <q-item class="text-center">
              <q-item-section>
                <q-input
                  outlined
                  lazy-rules
                  :rules="[
                    val => (val && val.length > 0) || 'Campo obligatorio'
                  ]"
                  stack-label
                  dense
                  v-model="correo"
                  ref="correo"
                  label="Correo electrónico"
                ></q-input>
              </q-item-section>
            </q-item>
            <q-item class="text-center">
              <q-item-section>
                <q-select
                  outlined
                  dense
                  clearable
                  v-model="tipo_documento"
                  :options="options_tipo_documento"
                  option-label="name"
                  option-value="value"
                  emit-value
                  stack-label
                  map-options
                  label="Tipo de documento"
                  lazy-rules
                  :rules="[val => (val && val > 0) || 'Campo obligatorio']"
                />
                <!-- <q-input
                  outlined
                  lazy-rules
                  :rules="[
                    val => (val && val.length === 8) || 'Campo obligatorio'
                  ]"
                  stack-label
                  dense
                  counter
                  maxlength="8"
                  v-model="numero_documento"
                  ref="tipo_documento"
                  label="Número de DNI *"
                ></q-input> -->
              </q-item-section>
              <q-item-section>
                <q-input
                  outlined
                  lazy-rules
                  :rules="[
                    val => (val && val.length >= conteo ) || 'Campo obligatorio'
                  ]"
                  stack-label
                  dense
                  counter
                  :maxlength=conteo
                  v-model="numero_documento"
                  ref="numero_documento"
                  label="Número de documento *"
                ></q-input>
              </q-item-section>
            </q-item>
            <q-item class="text-center">
              <q-item-section>
                <q-input
                  stack-label
                  outlined
                  label="Fecha de Nacimiento"
                  dense
                  v-model="fecha_nacimiento"
                  lazy-rules
                  :rules="[
                    val => (val && val.length > 0) || 'Campo obligatorio'
                  ]"
                >
                  <template v-slot:append>
                    <q-icon name="event" class="cursor-pointer">
                      <q-popup-proxy
                        ref="qDateProxy"
                        transition-show="scale"
                        transition-hide="scale"
                      >
                        <q-date mask="YYYY-MM-DD" default-view="Years" v-model="fecha_nacimiento">
                          <div class="row items-center justify-end">
                            <q-btn
                              v-close-popup
                              label="Close"
                              color="primary"
                              flat
                            />
                          </div>
                        </q-date>
                      </q-popup-proxy>
                    </q-icon>
                  </template>
                </q-input>
              </q-item-section>
              <q-item-section>
                <q-input
                  outlined
                  lazy-rules
                  :rules="[
                    val => (val && val.length === 9) || 'Campo obligatorio'
                  ]"
                  stack-label
                  dense
                  counter
                  maxlength="9"
                  v-model="celular"
                  ref="celular"
                  label="Celular *"
                ></q-input>
              </q-item-section>
            </q-item>
            <q-separator spaced inset />
            <q-item class="text-center">
              <q-item-section class="text-left q-pl-md">
                ¿Nacionalidad? *
                <q-option-group
                  dense
                  size="xs"
                  :options="optionsN"
                  label="¿Nacionalidad"
                  type="radio"
                  v-model="ti_nacion"
                  lazy-rules
                  :rules="[
                    val => (val && val.length > 0) || 'Campo obligatorio'
                  ]"
                />
              </q-item-section>
            </q-item>
          <q-separator spaced inset /> 
            <q-item class="text-center">
              <q-item-section class="text-left q-pl-md">
                ¿Estado Civil? *
                <q-option-group
                  dense
                  size="xs"
                  :options="optionsC"
                  label="Notifications"
                  type="radio"
                  v-model="estado_civil"
                  lazy-rules
                  :rules="[
                    val => (val && val.length > 0) || 'Campo obligatorio'
                  ]"
                />
              </q-item-section>
            </q-item> 
            <q-separator spaced inset />
            <q-item class="text-center">
              <q-item-section class="text-left q-pl-md">
                Tipo de licencia de conducir (Solo se acepta brevete peruano)
                <q-option-group
                  dense
                  size="xs"
                  :options="optionsLI"
                  type="radio"
                  v-model="ti_liccon"
                />
              </q-item-section>
            </q-item>
            <q-separator spaced inset />

            <q-item class="text-center">
              <q-item-section>
                <q-select
                  ref="region"
                  outlined
                  stack-label
                  dense
                  @input="getProv"
                  v-model="region"
                  :options="get_depart.result"
                  option-label="name"
                  option-value="id"
                  emit-value
                  map-options
                  label="Departamento:"
                  clearable
                  lazy-rules
                  :rules="[
                    val => (val && val.length > 0) || 'Campo obligatorio'
                  ]"
                />
                <!-- <q-select outlined  stack-label dense v-model="model" ref="model" label="¿En qué distrito vives? *"></q-select> -->
              </q-item-section>
              <q-item-section>
                <q-select
                  ref="ciudad"
                  dense
                  outlined
                  stack-label
                  @input="getDistri"
                  v-model="ciudad"
                  :options="get_provin.result"
                  option-value="id"
                  option-label="name"
                  emit-value
                  map-options
                  label="Provincia:"
                  clearable
                  lazy-rules
                  :rules="[
                    val => (val && val.length > 0) || 'Campo obligatorio'
                  ]"
                />
              </q-item-section>
            </q-item>
            <q-item class="text-center">
              <q-item-section>
                <q-select
                  ref="distrito"
                  dense
                  outlined
                  stack-label
                  v-model="distrito"
                  :options="get_distridistri.result"
                  option-value="id"
                  option-label="name"
                  emit-value
                  map-options
                  label="Distrito:"
                  clearable
                  lazy-rules
                  :rules="[
                    val => (val && val.length > 0) || 'Campo obligatorio'
                  ]"
                />
              </q-item-section>
            </q-item>
            <q-item class="text-center">
              <q-item-section avatar>
                <q-toggle style="align-self: center;" v-model="accept" />
              </q-item-section>
              <q-item-section class="cursor-pointer" @click="terminos">
                Acepta usted la Política de Tratamiento de datos personales
                https://bit.ly/2CvON7Q *
              </q-item-section>
            </q-item>
            <q-item class="text-center">
              <q-item-section>
                <q-btn
                  outline
                  color="green"
                  type="submit"
                  label="Enviar"
                  :loading="loadboton"
                ></q-btn>
              </q-item-section>
            </q-item>
          </q-form>
        </q-list>
      </div>
      <div class="col-md-3"></div>
    </div>
  </q-page>
</template>

<script>
export default {
  name: "PageIndex",
  data() {
    return {
      estado_civil : "",
      ti_nacion: "",
      tipo_documento: null,
      optionsLI: [
         {
          label: "A1",
          value: 1
        },
        {
          label: "A2",
          value: 2
        },
        {
          label: "A3",
          value: 4
        },
        {
          label: "Otro",
          value: 10
        },
      ],
      options_tipo_documento: [
        {
          name: "DNI",
          value: 1
        },
        {
          name: "C.E",
          value: 2
        },
        {
          name: "PTP",
          value: 3
        }
      ],
      group: null,
      optionsN: [
        { label: "Venezolana", value: "VE" },
        { label: "Peruana", value: "PE", color: "green" }
      ],
      optionsC: [
        { label: "Soltero", value: "S" },
        { label: "Casado", value: "C", color: "green" },
        {
          label: "Viudo",
          value: "V",
          color: "red"
        },
        {
          label: "Divorciado",
          value: "D",
          color: "orange"
        },
        {
          label: "Conviviente",
          value: "O",
          color: "teal"
        }
      ],
      optionsE: [
        { label: "Menos de 1 año", value: "1" },
        { label: "1 año", value: "2", color: "green" },
        {
          label: "Más de 1 año",
          value: "3",
          color: "red"
        },
        {
          label: "No tengo experiencia",
          value: "4",
          color: "orange"
        }
      ],
      optionsR: [
        { label: "B2C", value: "9" },
        { label: "Otro", value: "10", color: "green" },
        {
          label: "Brevete venezolano",
          value: "12",
          color: "red"
        },
        {
          label: "No tengo Brevete",
          value: "11",
          color: "orange"
        }
      ],
      loadboton: false,
      accept: false,
      submitResult: [],
      get_depart: "",
      get_provin: "",
      get_distridistri: "",
      region: "",
      experiencia: "",
      ciudad: "",
      distrito: "",
      model: "",
      apellido_paterno: "",
      apellido_materno: "",
      correo: "",
      nombres: "",
      numero_documento: "",
      fecha_nacimiento: "",
      celular: "",
      brevete: "",
      co_plaveh: "",
      co_modveh: "",
      ti_liccon: "",
      ti_vehper: "",
      ti_combus: "",
    };
  },
  computed: {
    conteo(){
      if (this.tipo_documento == 1) {
        return 8
      } else {
        return 9
      }
      
    }
  },
  methods: {
    terminos() {
      window.open("https://bit.ly/2CvON7Q");
    },
    async getProv() {
      const respon = await this.$axios.get(
        `https://api.apps.com.pe/sgsform/provin/${this.region}`
      );
      this.get_provin = respon.data;
      this.ciudad = "";
      this.distrito = "";
    },
    async getDistri() {
      const respon = await this.$axios.get(
        `https://api.apps.com.pe/sgsform/distri/${this.ciudad}`
      );
      this.get_distridistri = respon.data;
      this.distrito = "";
    },
    async onSubmit() {
      try {
        this.loadboton = true;
        if (this.accept) {
          const JsonEnviar = {
            // region: this.region,
            // ciudad: this.ciudad,
            // brevete: this.brevete,
            // lo que recibe el webservice
            ti_landin: 3,
            no_apepat: this.apellido_paterno ? this.apellido_paterno : "",
            no_apemat: this.apellido_materno ? this.apellido_materno : "",
            no_nombre: this.nombres ? this.nombres : "",
            co_docide: this.numero_documento ? this.numero_documento : "",
            ti_docide: this.tipo_documento ? this.tipo_documento : "",
            ti_nacion: this.ti_nacion ? this.ti_nacion : "",
            fe_nacimi: this.fecha_nacimiento,
            no_correo: this.correo ? this.correo : "",
            nu_telefo: this.celular ? this.celular : "",
            va_experi: this.experiencia ? this.experiencia : "",
            ti_liccon: this.ti_liccon ? this.ti_liccon : "",
            co_ubigeo: this.distrito ? this.distrito : "",
            co_plaveh: this.co_plaveh ? this.co_plaveh : "",
            co_modveh: this.co_modveh ? this.co_modveh : "",
            ti_vehper: this.ti_vehper ? this.ti_vehper : "",
            ti_combus: this.ti_combus ? this.ti_combus : "",
            co_estciv: this.estado_civil ? this.estado_civil : ""
          };
          console.log(JsonEnviar);
          const respon = await this.$axios.post(
            `https://api.reinventing.com.pe/v2.0/comerc/insert_landin`,
            JsonEnviar
          );
          // const respon = await this.$axios.post(
          //   `http://127.0.0.1:5001/api/v1.0/comerc/insert_landin`,
          //   JsonEnviar
          // );
          console.log("respon.data", respon.data);
          this.$q.notify({
            position: "top-right",
            message: "Registro Correcto",
            color: "green"
          });
          this.loadboton = false;
          setTimeout(() => {
            window.location.reload();
          }, 2000);
        } else {
          this.$q.notify({
            position: "top-right",
            message: "Debe aceptar los terminos y condiciones",
            color: "red"
          });
          this.loadboton = false;
        }
      } catch (e) {
        console.log(e);
        this.$q.notify({
          position: "top-right",
          message: "Oh oh..!! Comicate con nosotros algo salio mal",
          color: "red"
        });
        this.loadboton = false;
      }
    },
    paso(val) {
      if (val === 3) {
        this.$refs.nombres.validate();
        this.$refs.correo.validate();
        this.$refs.apellidos.validate();
        this.$refs.tipodocumento.validate();
        this.$refs.documentIdentidad.validate();
        this.$refs.fechaNacimiento.validate();
        this.$refs.correoElectronico.validate();
        this.$refs.teleCelular.validate();
        this.$refs.pais.validate();
        this.$refs.region.validate();
        this.$refs.ciudad.validate();
        this.$refs.distrito.validate();
        this.$refs.direccion.validate();
        this.$refs.enterarte.validate();
        if (
          this.$refs.nombres.hasError ||
          this.$refs.correo.hasError ||
          this.$refs.apellidos.hasError ||
          this.$refs.tipodocumento.hasError ||
          this.$refs.documentIdentidad.hasError ||
          this.$refs.fechaNacimiento.hasError ||
          this.$refs.correoElectronico.hasError ||
          this.$refs.teleCelular.hasError ||
          this.$refs.pais.hasError ||
          this.$refs.region.hasError ||
          this.$refs.ciudad.hasError ||
          this.$refs.distrito.hasError ||
          this.$refs.direccion.hasError ||
          this.$refs.enterarte.hasError
        ) {
          this.formHasError = true;
          return false;
        } else {
          // this.$q.notify({
          //   icon: "done",
          //   color: "positive",
          //   message: "Submitted"
          // });
          return true;
        }
      } else if (val === 4) {
        this.$refs.Industriaogiro.validate();
        this.$refs.areadondetrabaja.validate();
        this.$refs.Cargoopuesto.validate();
        this.$refs.Centrodetrabajo.validate();
        return !(
          this.$refs.Industriaogiro.hasError ||
          this.$refs.areadondetrabaja.hasError ||
          this.$refs.Cargoopuesto.hasError ||
          this.$refs.Centrodetrabajo.hasError
        );
      } else {
        return true;
      }
    }
  },
  async created() {
    const respon = await this.$axios.get(
      `https://api.apps.com.pe/sgsform/depart`
    );
    this.get_depart = respon.data;
  }
};
</script>
<style></style>
