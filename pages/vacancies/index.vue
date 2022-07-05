<template>
  <div class="vacancy">
    <header-h2
      v-if="vacanciesList"
      heading="Вакансии"
      is-main
      :left-line="true"
      :count="vacanciesList.length"
    />
    <div class="container">
      <header-h3 header-h3="с нами ты можешь:" />
      <div class="vacancy__youcan">
        <div
          v-for="(requirement, index) in requirements"
          :key="index"
          class="vacancy__youcan-block"
        >
          <img class="vacancy__youcan-img" :src="requirement.icon" alt="" />
          <div class="vacancy__youcan-text">{{ requirement.text }}</div>
        </div>
      </div>
      <div class="command">
        <div class="command__count">
          <div class="command__count-figure">
            <div class="command__count-elem">></div>
            <div class="command__count-employee">50</div>
          </div>
          <div class="command__count-text">человек в команде</div>
        </div>
        <div class="command__about">
          <div class="command__about-main">
            Присоединяйтесь к команде специалистов, помешанных на инновационном
            подходе во всем.
          </div>
          <div class="command__about-work">
            Для непрерывного развития мы создаем продукты в направлениях: EdTech
            (образование), HRTech (управление персоналом) и Data (управление
            данными).
          </div>
          <div class="command__about-tovacancy" @click="scroll">
            <div class="command__about-text">К вакансиям</div>
            <img
              class="command__about-img"
              src="~/assets/icons/Arrow.svg"
              alt=""
            />
          </div>
        </div>
        <content-line class="content-line">
          <template
            v-for="(command, index) in commands"
            :slot="`slot-${index}`"
          >
            <word-stroke :key="index" class="word-stroke">
              <div class="content">
                <div class="content__count">{{ command.count }}</div>
                <p class="content__text">{{ command.text }}</p>
              </div>
            </word-stroke>
          </template>
        </content-line>
      </div>
    </div>
    <header-h2 heading="Собеседование в ицрно" :left-line="true" />
    <div class="container">
      <div class="vacancy__stages">
        <div class="vacancy__stages-stage">
          <img
            class="vacancy__stages-img"
            src="~/assets/icons/Stage1.svg"
            alt=""
          />
          <header-h3
            class="vacancy__stages-head"
            header-h3="как попасть на собеседование"
          />
          <div class="vacancy__stages-info">
            <p class="vacancy__stages-text">
              Выберите подходящую вакансию и отправьте нам письмо через форму.
              Если вакансия предполагает тестовое задание - оно будет направлено
              по почте. В случае положительного решения с Вами свяжется наш
              сотрудник.
            </p>
            <p class="vacancy__stages-text">
              Если Вы хотите попасть к нам на <b>стажировку</b> - направьте
              информацию о себе в свободном формате на электронную почту
              admin@scieddi.ru
            </p>
          </div>
          <h4>Советы по резюме</h4>
          <p class="vacancy__stages-text">
            Рекомендуем направлять файл в <b>pdf</b> формате, а дизайнерам и
            разработчикам советуем включить в резюме активные ссылки на
            портфолио или на репозиторий. Можно сопроводить резюме парой
            предложений в о том, почему вам интересна работа у нас или другими
            деталями, которые вы считаете нужным сообщить на данном этапе
          </p>
          <h4>Тем, кто хочет попасть на стажировку</h4>
          <p class="vacancy__stages-text">
            Мы будем рады студентам последних курсов технических вузов, с
            неподдельным интересом к системе высшего образования, ярко
            выраженным желанием приносить пользу и развиваться.
          </p>
        </div>
        <div class="vacancy__stages-stage">
          <img
            class="vacancy__stages-img"
            src="~/assets/icons/Stage2.svg"
            alt=""
          />
          <header-h3
            class="vacancy__stages-head"
            header-h3="как проходит собеседование"
          />
          <p class="vacancy__stages-text">
            Первый этап собеседования проводит непосредственный руководитель и
            заместитель директора Института
            <b>(офлайн и онлайн собеседование).</b>
            Финальный этап за директором Института.
          </p>
          <h4>Советы по подготовке</h4>
          <p class="vacancy__stages-text">
            Будьте готовы привести в пример реальные кейсы из вашего
            профессионального опыта, поучаствовать в дискуссии на заданную тему,
            поделиться своим видением решения смоделированной задачи.
          </p>
          <p class="vacancy__stages-text">
            В случае успешного прохождения всех этапов с Вами свяжется наш
            сотрудник и озвучит предложение , а также детали по трудоустройству
            и оформлению документов по практике.
          </p>
        </div>
      </div>
      <div class="vacancy__card">
        <smart-link
          v-for="(vacancy, index) in vacanciesList"
          :key="index"
          :to="{ name: 'vacancies-id', params: { id: vacancy.id } }"
          class="card"
        >
          <card-up-line :style="{ width: '100%' }">
            <div>
              {{ vacancy.name }}
            </div>
          </card-up-line>
        </smart-link>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
  import {
    defineComponent,
    ref,
    Ref,
    SetupContext,
    useContext,
    useFetch,
  } from '@nuxtjs/composition-api';

  import commands from '../../scripts/commands';

  import HeaderH2 from '~/components/atoms/HeaderH2.vue';
  import HeaderH3 from '~/components/atoms/HeaderH3.vue';
  import CardUpLine from '~/components/molecules/CardUpLine.vue';
  import requirements from '~/scripts/requirements';
  import ContentLine from '~/components/ContentLine.vue';
  import WordStroke from '~/components/WordStroke.vue';
  import Default from '~/layouts/default.vue';
  import SmartLink from '~/components/SmartLink.vue';
  import Paragraph from '~/components/Paragraph.vue';

  export default defineComponent({
    head: {
      title: 'Работа в ИЦРНО',
      meta: [
        {
          hid: 'keywords',
          name: 'keywords',
          content:
            'работа, вакансии, работа в образовании, наука, стажировка, ищу работу, развитие, опыт, высшее образование',
        },
        {
          hid: 'description',
          name: 'description',
          content:
            'Команда ИЦРНО - это более 50 целеустремленных человек, работающих на благо российского высшего образования.',
        },
        {
          hid: 'og:title',
          name: 'og:title',
          content: 'Работа в ИЦРНО',
        },
        {
          hid: 'og:keywords',
          name: 'og:keywords',
          content:
            'работа, вакансии, работа в образовании, наука, стажировка, ищу работу, развитие, опыт, высшее образование',
        },
        {
          hid: 'og:description',
          name: 'og:description',
          content:
            'Команда ИЦРНО - это более 50 целеустремленных человек, работающих на благо российского высшего образования.',
        },
        {
          hid: 'og:image',
          name: 'og:image',
          content: `${process.env.VUE_APP_DOMAIN}/favicon-logo.png`,
        },
      ],
    },
    components: {
      Paragraph,
      SmartLink,
      Default,
      ContentLine,
      CardUpLine,
      HeaderH2,
      HeaderH3,
      WordStroke,
    },

    setup(_, context: SetupContext) {
      const { $axios } = useContext();

      const vacanciesList: Ref<null | unknown> = ref(null);

      useFetch(async () => {
        vacanciesList.value = await $axios
          .get(`/api/v1/vacancies`)
          .then((res: Record<'data', unknown>) => res.data);
      });

      // const vacanciesList = [
      //   'Менеджер проектов',
      //   'Аналитик',
      //   'Администратор',
      //   'Графический дизаин',
      //   'Дизайнер',
      //   'Frontend-разработчик',
      // ];

      function scroll() {
        const element =
          context.root.$el.getElementsByClassName('vacancy__card')[0];
        element.scrollIntoView({ behavior: 'smooth' });
      }

      return {
        commands,
        requirements,
        scroll,
        vacanciesList,
      };
    },
  });
</script>

<style lang="scss" scoped>
  @import './css/settings';
  @import './css/particles/paragraph';

  .vacancy {
    &__youcan {
      display: flex;
      flex-direction: column;
      padding-bottom: map-get($units, xsmall) * 31;
      padding-top: map-get($units, xsmall) * 74;

      &-block {
        display: flex;
        padding-bottom: map-get($units, xsmall) * 23;
      }

      &-img {
        padding-right: map-get($units, xsmall) * 30;
        //width: map-get($units, xsmall) * 41;
      }

      &-text {
        align-self: center;
        color: $white-color;
        display: flex;
        font-size: map-get($units, xsmall) * 14;
        font-weight: 400;
        line-height: map-get($units, xsmall) * 20;
      }
    }

    &__stages {
      border-bottom: $secondary-color map-get($units, xsmall) * 1 solid;
      display: grid;
      padding-bottom: map-get($units, xsmall) * 54;

      &-stage {
        color: $white-color;
        display: grid;
      }

      &-img {
        justify-self: center;
        padding-bottom: map-get($units, xsmall) * 35;
        width: map-get($units, xsmall) * 191;
      }

      &-head {
        padding-bottom: map-get($units, xsmall) * 65;
      }

      &-text {
        @include paragraph();

        padding-bottom: map-get($units, xsmall) * 30;
      }
    }

    & h4 {
      font-size: map-get($units, xsmall) * 20;
      font-weight: 700;
      line-height: map-get($units, xsmall) * 30;
      padding-bottom: map-get($units, xsmall) * 16;
    }

    &__card {
      padding-top: map-get($units, xsmall) * 50;
      padding-bottom: map-get($units, xsmall) * 80;

      & > * {
        display: block;
      }

      .card {
        cursor: pointer;
        font-size: map-get($units, xsmall) * 16;
        font-weight: 400;
        height: map-get($units, xsmall) * 104;
        line-height: map-get($units, xsmall) * 30;
        margin-bottom: map-get($units, xsmall) * 20;
        width: 100%;
      }

      .smart-link:visited {
        color: $white-color;
      }
    }
  }

  .command {
    padding-bottom: map-get($units, xsmall) * 56;

    &__count {
      &-figure {
        display: flex;
        justify-content: center;
      }

      &-elem {
        align-self: center;
        color: $secondary-color;
        font-family: 'Play', sans-serif;
        font-size: map-get($units, xsmall) * 48;
        font-weight: 700;
        line-height: map-get($units, xsmall) * 54;
        padding-right: map-get($units, xsmall) * 3;
      }

      &-employee {
        color: $secondary-color;
        font-family: 'Play', sans-serif;
        font-size: map-get($units, xsmall) * 150;
        font-weight: 700;
        line-height: map-get($units, xsmall) * 198;
      }

      &-text {
        color: $white-color;
        display: flex;
        font-size: map-get($units, xsmall) * 22;
        font-weight: 400;
        justify-content: center;
        line-height: map-get($units, xsmall) * 34;
        padding-bottom: map-get($units, xsmall) * 30;
      }
    }

    &__about {
      padding-bottom: map-get($units, xsmall) * 30;

      &-main {
        color: $white-color;
        font-size: map-get($units, xsmall) * 16;
        font-weight: 700;
        line-height: map-get($units, xsmall) * 24;
        padding-bottom: map-get($units, xsmall) * 20;
      }

      &-work {
        color: $white-color;
        font-size: map-get($units, xsmall) * 14;
        font-weight: 400;
        line-height: map-get($units, xsmall) * 24;
        padding-bottom: map-get($units, xsmall) * 20;
      }

      &-tovacancy {
        cursor: pointer;
        display: flex;
      }

      &-text {
        color: $secondary-color;
        font-size: map-get($units, xsmall) * 14;
        padding-right: map-get($units, xsmall) * 8;
      }

      &-img {
        align-self: center;
        display: flex;
      }
    }
  }

  .content {
    font-family: 'Play', sans-serif;

    &__count {
      color: $white-color;
      font-size: map-get($units, xsmall) * 37;
      font-weight: 700;
      line-height: map-get($units, xsmall) * 83;
    }

    &__text {
      color: $white-color;
      font-weight: 700;
      font-size: map-get($units, xsmall) * 12;
      line-height: map-get($units, xsmall) * 18;
      padding-bottom: initial;
    }
  }

  @include breakpoint(small) {
    .vacancy {
      &__youcan {
        padding-bottom: map-get($units, small) * 77;
        padding-top: map-get($units, small) * 77;

        &-block {
          padding-bottom: map-get($units, small) * 35;
        }

        &-img {
          padding-right: map-get($units, small) * 30;
          //width: map-get($units, small) * 52;
        }

        &-text {
          font-size: map-get($units, small) * 16;
          line-height: map-get($units, small) * 26;
        }
      }

      &__stages {
        border-width: map-get($units, small) * 1;
        padding-bottom: map-get($units, small) * 79;

        &-img {
          padding-bottom: map-get($units, small) * 50;
          width: map-get($units, small) * 221;
        }

        &-head {
          padding-bottom: map-get($units, small) * 80;
        }

        &-text {
          padding-bottom: map-get($units, small) * 30;
        }
      }

      & h4 {
        font-size: map-get($units, small) * 26;
        line-height: map-get($units, small) * 30;
        padding-bottom: map-get($units, small) * 16;
      }

      &__card {
        display: flex;
        grid-column-gap: map-get($units, small) * 15;
        flex-flow: wrap;
        padding-top: map-get($units, small) * 89;
        padding-bottom: map-get($units, small) * 72;

        .card {
          font-size: map-get($units, small) * 16;
          height: map-get($units, small) * 156;
          line-height: map-get($units, small) * 30;
          margin-bottom: map-get($units, small) * 38;
          width: 48%;
        }
      }
    }

    .command {
      display: grid;
      grid-template-areas:
        'count about'
        'elipse elipse';
      grid-template-columns: 1fr 1fr;
      padding-bottom: map-get($units, small) * 81;

      &__count {
        grid-area: count;

        &-elem {
          font-size: map-get($units, small) * 48;
          line-height: map-get($units, small) * 54;
          padding-right: map-get($units, small) * 3;
        }

        &-employee {
          font-size: map-get($units, small) * 150;
          line-height: map-get($units, small) * 198;
        }

        &-text {
          font-size: map-get($units, small) * 22;
          line-height: map-get($units, small) * 34;
          padding-bottom: map-get($units, small) * 30;
        }
      }

      &__about {
        grid-area: about;
        padding-top: map-get($units, small) * 40;
        padding-bottom: map-get($units, small) * 38;

        &-main {
          font-size: map-get($units, small) * 16;
          line-height: map-get($units, small) * 24;
          padding-bottom: map-get($units, small) * 20;
        }

        &-work {
          font-size: map-get($units, small) * 14;
          line-height: map-get($units, small) * 24;
          padding-bottom: map-get($units, small) * 20;
        }

        &-text {
          font-size: map-get($units, small) * 14;
          padding-right: map-get($units, small) * 8;
        }
      }

      .content-line {
        grid-area: elipse;
      }

      .content {
        &__count {
          font-size: map-get($units, small) * 37;
          line-height: map-get($units, small) * 83;
        }

        &__text {
          font-size: map-get($units, small) * 12;
          line-height: map-get($units, small) * 18;
          padding-bottom: initial;
        }
      }
    }
  }

  @include breakpoint(medium) {
    .vacancy {
      &__youcan {
        display: grid;
        grid-template-columns: 1fr 1fr;
        grid-row-gap: map-get($units, medium) * 20;
        padding-bottom: map-get($units, medium) * 129;
        padding-top: map-get($units, medium) * 122;

        &-block {
          padding-bottom: map-get($units, medium) * 35;
          padding-right: map-get($units, medium) * 30;
        }

        &-img {
          padding-right: map-get($units, medium) * 30;
          //width: map-get($units, medium) * 52;
        }

        &-text {
          font-size: map-get($units, medium) * 16;
          line-height: map-get($units, medium) * 26;
        }
      }

      &__stages {
        border-width: map-get($units, medium) * 1;
        padding-bottom: map-get($units, medium) * 80;

        &-img {
          padding-bottom: map-get($units, medium) * 50;
          width: map-get($units, medium) * 221;
        }

        &-head {
          padding-bottom: map-get($units, medium) * 80;
        }

        &-text {
          padding-bottom: map-get($units, medium) * 30;
        }
      }

      & h4 {
        font-size: map-get($units, medium) * 26;
        line-height: map-get($units, medium) * 30;
        padding-bottom: map-get($units, medium) * 16;
      }

      &__card {
        padding-top: map-get($units, medium) * 89;
        padding-bottom: map-get($units, medium) * 72;

        .card {
          font-size: map-get($units, medium) * 20;
          height: map-get($units, medium) * 156;
          line-height: map-get($units, medium) * 30;
          margin-bottom: map-get($units, medium) * 39;
          width: 48%;
        }
      }
    }

    .command {
      padding-bottom: map-get($units, medium) * 95;

      &__count {
        &-elem {
          font-size: map-get($units, medium) * 48;
          line-height: map-get($units, medium) * 54;
          padding-right: map-get($units, medium) * 3;
        }

        &-employee {
          font-size: map-get($units, medium) * 150;
          line-height: map-get($units, medium) * 198;
        }

        &-text {
          font-size: map-get($units, medium) * 22;
          line-height: map-get($units, medium) * 34;
          padding-bottom: map-get($units, medium) * 30;
        }
      }

      &__about {
        padding-top: initial;
        padding-bottom: map-get($units, medium) * 45;

        &-main {
          font-size: map-get($units, medium) * 18;
          line-height: map-get($units, medium) * 24;
          padding-bottom: map-get($units, medium) * 20;
        }

        &-work {
          font-size: map-get($units, medium) * 16;
          line-height: map-get($units, medium) * 24;
          padding-bottom: map-get($units, medium) * 20;
        }

        &-text {
          font-size: map-get($units, medium) * 14;
          padding-right: map-get($units, medium) * 8;
        }
      }

      .content {
        &__count {
          font-size: map-get($units, medium) * 37;
          line-height: map-get($units, medium) * 83;
        }

        &__text {
          font-size: map-get($units, medium) * 12;
          line-height: map-get($units, medium) * 18;
          padding-bottom: initial;
        }
      }
    }
  }

  @include breakpoint(large) {
    .vacancy {
      &__youcan {
        grid-row-gap: map-get($units, large) * 20;
        padding-bottom: map-get($units, large) * 120;
        padding-top: map-get($units, large) * 102;

        &-block {
          padding-bottom: map-get($units, large) * 35;
          padding-right: map-get($units, large) * 30;
        }

        &-img {
          padding-right: map-get($units, large) * 30;
          //width: map-get($units, large) * 52;
        }

        &-text {
          font-size: map-get($units, large) * 16;
          line-height: map-get($units, large) * 26;
        }
      }

      &__stages {
        border-width: map-get($units, large) * 1;
        padding-bottom: map-get($units, large) * 86;

        &-img {
          padding-bottom: map-get($units, large) * 50;
          width: map-get($units, large) * 221;
        }

        &-head {
          padding-bottom: map-get($units, large) * 60;
        }

        &-text {
          padding-bottom: map-get($units, large) * 30;
        }
      }

      & h4 {
        font-size: map-get($units, large) * 26;
        line-height: map-get($units, large) * 30;
        padding-bottom: map-get($units, large) * 16;
      }

      &__card {
        grid-column-gap: map-get($units, large) * 18;
        padding-top: map-get($units, large) * 88;
        padding-bottom: map-get($units, large) * 80;

        .card {
          font-size: map-get($units, large) * 20;
          height: map-get($units, large) * 156;
          line-height: map-get($units, large) * 30;
          margin-bottom: map-get($units, large) * 35;
          width: 32%;
        }
      }
    }

    .command {
      padding-bottom: map-get($units, large) * 95;
      grid-template-columns: 30% 1fr;
      grid-column-gap: map-get($units, large) * 76;

      &__count {
        &-elem {
          font-size: map-get($units, large) * 68;
          line-height: map-get($units, large) * 54;
          padding-right: map-get($units, large) * 3;
        }

        &-employee {
          font-size: map-get($units, large) * 177;
          line-height: map-get($units, large) * 198;
        }

        &-text {
          font-size: map-get($units, large) * 26;
          line-height: map-get($units, large) * 34;
          padding-bottom: map-get($units, large) * 30;
        }
      }

      &__about {
        padding-top: map-get($units, large) * 40;
        padding-bottom: map-get($units, large) * 45;

        &-main {
          font-size: map-get($units, large) * 18;
          line-height: map-get($units, large) * 24;
          padding-bottom: map-get($units, large) * 20;
          padding-right: map-get($units, large) * 5;
        }

        &-work {
          font-size: map-get($units, large) * 16;
          line-height: map-get($units, large) * 24;
          padding-bottom: map-get($units, large) * 20;
        }

        &-text {
          font-size: map-get($units, large) * 14;
          padding-right: map-get($units, large) * 8;
        }
      }

      .content {
        &__count {
          font-size: map-get($units, large) * 37;
          line-height: map-get($units, large) * 83;
        }

        &__text {
          font-size: map-get($units, large) * 12;
          line-height: map-get($units, large) * 18;
          padding-bottom: initial;
        }
      }
    }
  }

  @include breakpoint(xlarge) {
    .vacancy {
      &__youcan {
        grid-column-gap: map-get($units, xlarge) * 210;
        grid-row-gap: map-get($units, xlarge) * 20;
        padding-bottom: map-get($units, xlarge) * 120;
        padding-top: map-get($units, xlarge) * 107;

        &-block {
          padding-bottom: map-get($units, xlarge) * 35;
          padding-right: map-get($units, xlarge) * 30;
        }

        &-img {
          padding-right: map-get($units, xlarge) * 30;
          //width: map-get($units, xlarge) * 52;
        }

        &-text {
          font-size: map-get($units, xlarge) * 16;
          line-height: map-get($units, xlarge) * 26;
        }
      }

      &__stages {
        border-width: map-get($units, xlarge) * 1;
        padding-bottom: map-get($units, xlarge) * 90;

        &-img {
          padding-bottom: map-get($units, xlarge) * 50;
          width: map-get($units, xlarge) * 221;
        }

        &-head {
          padding-bottom: map-get($units, xlarge) * 60;
        }

        &-text {
          padding-bottom: map-get($units, xlarge) * 30;
        }
      }

      & h4 {
        font-size: map-get($units, xlarge) * 26;
        line-height: map-get($units, xlarge) * 30;
        padding-bottom: map-get($units, xlarge) * 16;
      }

      &__card {
        grid-column-gap: map-get($units, xlarge) * 24;
        padding-top: map-get($units, xlarge) * 88;
        padding-bottom: map-get($units, xlarge) * 80;

        .card {
          font-size: map-get($units, xlarge) * 22;
          height: map-get($units, xlarge) * 156;
          line-height: map-get($units, xlarge) * 30;
          margin-bottom: map-get($units, xlarge) * 35;
          width: 32%;
        }
      }
    }

    .command {
      grid-template-columns: 21% 1fr;
      padding-bottom: map-get($units, xlarge) * 150;

      &__count {
        &-elem {
          font-size: map-get($units, xlarge) * 68;
          line-height: map-get($units, xlarge) * 54;
          padding-right: map-get($units, xlarge) * 3;
        }

        &-employee {
          font-size: map-get($units, xlarge) * 177;
          line-height: map-get($units, xlarge) * 198;
        }

        &-text {
          font-size: map-get($units, xlarge) * 26;
          line-height: map-get($units, xlarge) * 34;
          padding-bottom: map-get($units, xlarge) * 30;
        }
      }

      &__about {
        padding-top: map-get($units, xlarge) * 30;
        padding-bottom: map-get($units, xlarge) * 58;

        &-main {
          font-size: map-get($units, xlarge) * 18;
          line-height: map-get($units, xlarge) * 20;
          padding-bottom: map-get($units, xlarge) * 20;
          padding-right: map-get($units, xlarge) * 5;
        }

        &-work {
          font-size: map-get($units, xlarge) * 16;
          line-height: map-get($units, xlarge) * 20;
          padding-bottom: map-get($units, xlarge) * 20;
        }

        &-text {
          font-size: map-get($units, xlarge) * 16;
          padding-right: map-get($units, xlarge) * 8;
        }
      }

      .content-line {
        grid-column: 2;
      }

      .content {
        &__count {
          font-size: map-get($units, xlarge) * 37;
          line-height: map-get($units, xlarge) * 83;
        }

        &__text {
          font-size: map-get($units, xlarge) * 12;
          line-height: map-get($units, xlarge) * 18;
          padding-bottom: initial;
        }
      }
    }
  }

  @include breakpoint(xxlarge) {
    .vacancy {
      &__youcan {
        grid-column-gap: map-get($units, xxlarge) * 20;
        grid-row-gap: map-get($units, xxlarge) * 5;
        padding-bottom: map-get($units, xxlarge) * 120;
        padding-top: map-get($units, xxlarge) * 107;

        &-block {
          padding-bottom: map-get($units, xxlarge) * 35;
          padding-right: map-get($units, xxlarge) * 100;
          padding-left: map-get($units, xxlarge) * 110;
        }

        &-img {
          padding-right: map-get($units, xxlarge) * 30;
          //width: map-get($units, xxlarge) * 52;
        }

        &-text {
          font-size: map-get($units, xxlarge) * 16;
          line-height: map-get($units, xxlarge) * 26;
        }
      }

      &__stages {
        border-width: map-get($units, xxlarge) * 1;
        padding-bottom: map-get($units, xxlarge) * 90;

        &-img {
          padding-bottom: map-get($units, xxlarge) * 50;
          width: map-get($units, xxlarge) * 221;
        }

        &-head {
          padding-bottom: map-get($units, xxlarge) * 60;
        }

        &-text {
          padding-bottom: map-get($units, xxlarge) * 30;
        }
      }

      & h4 {
        font-size: map-get($units, xxlarge) * 26;
        line-height: map-get($units, xxlarge) * 30;
        padding-bottom: map-get($units, xxlarge) * 16;
      }

      &__card {
        grid-column-gap: map-get($units, xxlarge) * 14;
        padding-top: map-get($units, xxlarge) * 88;
        padding-bottom: map-get($units, xxlarge) * 80;

        .card {
          font-size: map-get($units, xxlarge) * 22;
          height: map-get($units, xxlarge) * 156;
          line-height: map-get($units, xxlarge) * 30;
          margin-bottom: map-get($units, xxlarge) * 31;
          width: 24%;
        }
      }
    }

    .command {
      padding-bottom: map-get($units, xxlarge) * 150;
      grid-template-columns: 20% 1fr;

      &__count {
        &-elem {
          font-size: map-get($units, xxlarge) * 68;
          line-height: map-get($units, xxlarge) * 54;
          padding-right: map-get($units, xxlarge) * 3;
        }

        &-employee {
          font-size: map-get($units, xxlarge) * 177;
          line-height: map-get($units, xxlarge) * 198;
        }

        &-text {
          font-size: map-get($units, xxlarge) * 26;
          line-height: map-get($units, xxlarge) * 34;
          padding-bottom: map-get($units, xxlarge) * 30;
        }
      }

      &__about {
        padding-top: map-get($units, xxlarge) * 40;
        padding-bottom: map-get($units, xxlarge) * 68;

        &-main {
          font-size: map-get($units, xxlarge) * 18;
          line-height: map-get($units, xxlarge) * 20;
          padding-bottom: map-get($units, xxlarge) * 20;
          padding-right: map-get($units, xxlarge) * 5;
        }

        &-work {
          font-size: map-get($units, xxlarge) * 16;
          line-height: map-get($units, xxlarge) * 20;
          padding-bottom: map-get($units, xxlarge) * 20;
        }

        &-text {
          font-size: map-get($units, xxlarge) * 16;
          padding-right: map-get($units, xxlarge) * 8;
        }
      }

      .content {
        &__count {
          font-size: map-get($units, xxlarge) * 37;
          line-height: map-get($units, xxlarge) * 83;
        }

        &__text {
          font-size: map-get($units, xxlarge) * 12;
          line-height: map-get($units, xxlarge) * 18;
          padding-bottom: initial;
        }
      }
    }
  }
</style>
