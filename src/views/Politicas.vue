<template>
    <div class="Terms">
      <Navigator />
      <div class="bodytyc">
        <div class="tituloc">
          <p class="t">Política de Privacidad</p>
          <img src="../assets/flowers-mo.svg" alt="mo" class="mo" />
          <img src="../assets/flowers-pc.svg" alt="pc" class="pc" />
        </div>
        <div class="sectxt">

        <p>Aviso de Privacidad Integral</p>
        <p>1. Identidad y domicilio del responsable</p>
<p>
[Nombre de la empresa o entidad responsable] ("la Empresa"), con domicilio en [Dirección completa], es responsable del tratamiento de sus datos personales.</p>
<p>Datos personales y finalidades del tratamiento
</p>
<p>La Empresa recaba y trata sus datos personales con las siguientes finalidades:</p>
<p class="txt2">Proveer los productos y servicios solicitados. <br>
Enviar comunicaciones comerciales y promocionales. <br>
Realizar actividades de mercadotecnia, publicidad y prospección comercial.<br>
Mejorar nuestros productos y servicios.<br>
</p>
<p>La información personal que obtenemos incluye, pero no se limita a: nombre, domicilio, teléfono, correo electrónico, RFC y datos de facturación.
</p>
<p>1. Transferencia de datos personales</p>
<p>La Empresa comparte sus datos personales con terceros exclusivamente para fines comerciales. Al aceptar este Aviso de Privacidad, usted otorga su consentimiento para que sus datos personales sean transferidos a terceros, siempre y cuando el tercero cumpla con las medidas de seguridad y confidencialidad adecuadas.
</p>
<p>1. Ejercicio de derechos ARCO y revocación del consentimiento
</p>
<p>Usted tiene derecho a acceder, rectificar y cancelar sus datos personales, así como a oponerse al tratamiento de los mismos o revocar el consentimiento que haya otorgado para tal fin. Para ejercer sus derechos ARCO y/o revocar su consentimiento, deberá enviar una solicitud por escrito a [Correo electrónico de contacto] con la siguiente información:
</p>
<p class="txt2">Nombre completo. <br>
Correo electrónico y/o teléfono para recibir notificaciones.<br>
Copia de su identificación oficial.<br>
Descripción detallada de los datos personales respecto de los que busca ejercer alguno de los derechos ARCO o revocar su consentimiento.<br>
Cualquier otro elemento o documento que facilite la localización de los datos personales.<br>
</p>
<p>La Empresa responderá su solicitud en un plazo máximo de 20 días hábiles.
</p>
<p>1. Cambios al Aviso de Privacidad</p>
<p>La Empresa se reserva el derecho de efectuar en cualquier momento modificaciones o actualizaciones al presente Aviso de Privacidad. Estas modificaciones estarán disponibles al público a través de nuestra página web [URL de la página web donde se encuentra el Aviso de Privacidad].
</p>
<p>1. Uso de cookies y tecnologías de seguimiento</p>
<p>La Empresa utiliza cookies y otras tecnologías de seguimiento en su página web para recabar información sobre las preferencias de los usuarios y mejorar su experiencia en línea. Al utilizar nuestro sitio web, usted acepta el uso de estas tecnologías.
</p>
<p>La Empresa utiliza cookies y otras tecnologías de seguimiento en su página web para recabar información sobre las preferencias de los usuarios y mejorar su experiencia en línea. Al utilizar nuestro sitio web, usted acepta el uso de estas tecnologías.
</p>
<p>1. Contacto</p>
<p>Si tiene alguna duda o comentario respecto al presente Aviso de Privacidad, por favor comuníquese con nosotros a través de [Correo electrónico de contacto].
Fecha de última actualización: [Fecha de actual</p>

        </div>
      </div>
      <Footer />
    </div>
  </template>
  <script>
  import Navigator from "../components/Navigator";
  import Footer from "../components/Footer";
  export default {
    name: "Terms",
    components: {
      Navigator,
      Footer,
    },
    metaInfo() {
      return {
        title: "Política de Privacidad",
        titleTemplate: "%s | Coyotas Lourdes",
        htmlAttrs: {
          lang: "es",
        },
        meta: [
          { charset: "utf-8" },
          {
            name: "description",
            content: "Coyotas Lourdes.",
          },
          { name: "viewport", content: "width=device-width, initial-scale=1" },
        ],
      };
    },
  };
  </script>
  <style>
  p {
    margin: 0;
  }
  a {
    font-weight: 500;
  }
  .bodytyc {
    padding: 36.957vw 0 16.184vw;
  }
  .tituloc img {
    width: 100%;
  }
  .tituloc .pc {
    display: none;
  }
  .tituloc .mo {
    display: block;
  }
  .tituloc .t {
    font-family: var(--font-titulo1);
    font-weight: 800;
    font-size: 8.454vw;
    line-height: 90.5%;
    text-align: center;
    color: #ff4713;
    width: 48.792vw;
    margin: auto;
  }
  .sectxt {
    width: 75.362vw;
    margin: 20.048vw auto 0;
  }

  .txt2{
    font-family: var(--font-titulo2);
    font-weight: 400;
    font-size: 5.314vw;
    line-height: 7.971vw;
    margin-bottom: 8vw;
    color: #909090;
    list-style-type: disc;
  }
  .sectxt p {
    font-family: var(--font-titulo2);
    font-weight: 400;
    font-size: 5.314vw;
    line-height: 7.971vw;
    margin-bottom: 8vw;
    color: #909090;
  }
  @media (min-width: 768px) {
    .bodytyc {
      padding: 17.135vw 0 9.427vw;
    }
    .tituloc .pc {
      display: block;
    }
    .tituloc .mo {
      display: none;
    }
    .tituloc .t {
      width: 100%;
      font-size: 3.802vw;
      line-height: 90.5%;
      margin-bottom: 4.427vw;
    }
    .sectxt {
      margin: 5.365vw auto 0;
    }
    .sectxt p {
      font-size: 1.042vw;
      line-height: 1.042vw;
      margin-bottom: 1vw;
    }

    .txt2 {
      font-size: 1.042vw;
      line-height: 1.042vw;
      margin-bottom: 1vw;
      list-style-type: disc;

    }
  }
  </style>