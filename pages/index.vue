<template>
  <div v-if="typesList && activities">
    <header-h2 left-line is-main heading="календарь мероприятий" />
    <!--    <div class="container">-->
    <!--      <div class="filter">-->
    <!--        <div class="events">-->
    <!--          <div class="events__menu">-->
    <!--            &lt;!&ndash;            <div class="events__menu-text" @click="changeAll">Выбрать все</div>&ndash;&gt;-->
    <!--            <div v-if="typesList && list.length > 0" class="events__menu-reset">-->
    <!--              <div class="events__menu-text" @click="deleteAll">-->
    <!--                Сбросить все-->
    <!--              </div>-->
    <!--              <img class="events__menu-icon" src="~/assets/close.svg" alt="" />-->
    <!--            </div>-->
    <!--          </div>-->
    <!--          <div v-if="typesList && list.length > 0" class="events__select">-->
    <!--            <div class="events__select-text">Выбрано:</div>-->
    <!--            <div-->
    <!--              v-for="(item, index) in list"-->
    <!--              :key="index"-->
    <!--              class="events__select-icon"-->
    <!--              :style="{ color: item, fontSize: '25px' }"-->
    <!--            >-->
    <!--              &#9679;-->
    <!--            </div>-->
    <!--          </div>-->
    <!--        </div>-->
    <!--        <div class="events__network">-->
    <!--          <div class="network">-->
    <!--            <div class="events__network-online">-->
    <!--              <img-->
    <!--                class="events__network-icon"-->
    <!--                src="~/assets/no-wifi.svg"-->
    <!--                alt=""-->
    <!--              />-->
    <!--              <div-->
    <!--                class="events__network-text"-->
    <!--                :class="{ active: filterOnline }"-->
    <!--                @click="selectOnline"-->
    <!--              >-->
    <!--                Online-->
    <!--              </div>-->
    <!--            </div>-->
    <!--            <div class="events__network-offline">-->
    <!--              <img-->
    <!--                class="events__network-icon"-->
    <!--                src="~/assets/wifi.svg"-->
    <!--                alt=""-->
    <!--              />-->
    <!--              <div-->
    <!--                class="events__network-text"-->
    <!--                :class="{ active: filterOffline }"-->
    <!--                @click="selectOffline"-->
    <!--              >-->
    <!--                Offline-->
    <!--              </div>-->
    <!--            </div>-->
    <!--            <div class="events__network-all">-->
    <!--              <img-->
    <!--                class="events__network-icon"-->
    <!--                src="~/assets/allRound.svg"-->
    <!--                alt=""-->
    <!--              />-->
    <!--              <div class="events__network-text" @click="selectAll">Все</div>-->
    <!--            </div>-->
    <!--          </div>-->
    <!--          &lt;!&ndash;          <div class="events__network-date">{{ localDate }}</div>&ndash;&gt;-->
    <!--        </div>-->
    <!--      </div>-->
    <!--      <div v-if="typesList" class="filters">-->
    <!--        <div-->
    <!--          v-for="(item, index) in typesList"-->
    <!--          :key="index"-->
    <!--          class="filters__checkbox"-->
    <!--        >-->
    <!--          <div class="filters__block">-->
    <!--            <input-->
    <!--              v-model="checkedTypes"-->
    <!--              :value="item.id"-->
    <!--              class="filters__checkbox-input"-->
    <!--              type="checkbox"-->
    <!--              :style="{ backgroundColor: item.color }"-->
    <!--              @click="addCheckedType(item)"-->
    <!--            />-->
    <!--          </div>-->
    <!--          <label-->
    <!--            class="filters__checkbox-text"-->
    <!--            :class="{ boldText: checkedTypes.some((el) => el === item.id) }"-->
    <!--            @click="addCheckedType(item)"-->
    <!--          >-->
    <!--            {{ item.content }}-->
    <!--          </label>-->
    <!--        </div>-->
    <!--      </div>-->
    <!--      &lt;!&ndash;      <div class="button__up">&ndash;&gt;-->
    <!--      &lt;!&ndash;        <img&ndash;&gt;-->
    <!--      &lt;!&ndash;          class="button__up-icon"&ndash;&gt;-->
    <!--      &lt;!&ndash;          src="~/assets/icons/roundButtonUp.svg"&ndash;&gt;-->
    <!--      &lt;!&ndash;          alt=""&ndash;&gt;-->
    <!--      &lt;!&ndash;        />&ndash;&gt;-->
    <!--      &lt;!&ndash;      </div>&ndash;&gt;-->
    <!--    </div>-->
    <div>
      <!--      <lazy-load-canvas v-model="lazyLoadOptions" :load-data="loadPage">-->
      <div
        v-for="(month, index) in eventsOfMonth"
        :id="`slot-${month.month}`"
        :key="`slot-${index}`"
        :slot="`slot-${index}`"
        class="test"
      >
        <event-month :event-list="month.events" />
      </div>
      <!--      </lazy-load-canvas>-->
    </div>
    <!--    <div class="button__down">-->
    <!--      <img-->
    <!--        class="button__down-icon"-->
    <!--        src="~/assets/icons/roundButtonDown.svg"-->
    <!--        alt=""-->
    <!--      />-->
    <!--    </div>-->
  </div>
</template>

<script lang="ts">
  import {
    computed,
    defineComponent,
    ref,
    Ref,
    useContext,
    useFetch,
  } from '@nuxtjs/composition-api';
  import events from '@/scripts/EventsMock';

  import LazyLoadCanvas from '~/components/LazyLoadCanvas.vue';
  import LazyLoadValue from '~/models/LazyLoadValue';
  import HeaderH2 from '~/components/atoms/HeaderH2.vue';
  import EventMonth from '~/components/blocks/EventMonth.vue';
  import colorRounds from '~/scripts/colorRounds';
  import {
    ICurrentEvent,
    IEventType,
    IEvent,
    IResponse,
  } from '~/scripts/models/event';

  export default defineComponent({
    components: {
      HeaderH2,
      LazyLoadCanvas,
      EventMonth,
    },
    setup() {
      const { $axios } = useContext();

      // eslint-disable-next-line camelcase
      const per_page = 400; // 4;

      // Получение типов мероприятий
      const typesList: Ref<null | IEventType[]> = ref(null);
      useFetch(async () => {
        typesList.value = await $axios
          .get(`/api/v1/activity_types.json`)
          .then((res: Record<'data', Record<'data', IEventType[]>>) => {
            return res.data.data;
          });
      });

      // Получение текущего мероприятия
      const currentEvent: Ref<null | ICurrentEvent> = ref(null);
      const activities: Ref<null | IEvent[]> = ref(null);

      // Состояние чекбоксов фильтров мероприятий
      const checkedTypes: Ref<number[]> = ref([]);

      const isTypeExist = (val: number): boolean => {
        return checkedTypes.value.some((el) => el === val);
      };

      // Массив цветов для отрисовки фильтрации по типам
      const list: Ref<string[]> = ref([]);

      const isOnline: Ref<null | boolean> = ref(null);

      const getEvents = (page: number) => {
        return $axios
          .get(`/api/v1/activities.json`, {
            params: {
              page,
              per_page,
              types: checkedTypes.value,
              is_online: isOnline.value === null ? undefined : isOnline.value,
            },
          })
          .then((res: IResponse) => {
            lazyLoadOptions.value.total = res.data.meta.all;

            // console.log('222', res);
            return res.data.data;
          });
      };

      // Метод получения событий определенного типа
      const getCheckedTypeEvents = async () => {
        await $axios
          .get(`/api/v1/activity/current_page.json`, {
            params: {
              per_page,
              types: checkedTypes.value,
              is_online: isOnline.value === null ? undefined : isOnline.value,
            },
          })
          .then(async (res: Record<'data', Record<'data', ICurrentEvent>>) => {
            currentEvent.value = res.data.data;
            if (currentEvent.value) {
              lazyLoadOptions.value = new LazyLoadValue(
                currentEvent.value.current_page,
                2,
              );
              activities.value = await getEvents(
                currentEvent.value.current_page,
              );
            }
          });
        // activities.value = await getEvents(currentEvent.value.current_page);
      };

      const addCheckedType = (val: IEventType) => {
        if (isTypeExist(val.id)) {
          checkedTypes.value = checkedTypes.value.filter((el) => el !== val.id);
          list.value = list.value.filter((el) => el !== val.color);
          getCheckedTypeEvents();
        } else {
          checkedTypes.value.push(val.id);
          list.value.push(val.color);
          getCheckedTypeEvents();
        }
      };

      const deleteAll = () => {
        checkedTypes.value = [];
        list.value = [];
        getCheckedTypeEvents();
      };

      // сортировка мероприятий по месяцам
      const eventsOfMonth = computed(() => {
        if (activities.value) {
          const arr = [];
          for (let i = 0; i < 12; i++) {
            const tempArr = activities.value.filter(
              (event) => new Date(event.started_at).getMonth() === i,
            );
            if (tempArr.length > 0) {
              arr.push({ month: i, events: tempArr });
            }
          }
          return arr;
        }
      });

      // код для Lazy Loading
      const eventsList: Ref<string[]> = ref([]);
      // const total = ref(0);
      //
      // const currentPage = randomRange(0, events.length - 1);

      const loadPage = (pageNum: number, callback: (arg0: number) => void) => {
        getEvents(pageNum).then((events) => {
          if (
            currentEvent.value &&
            pageNum > currentEvent.value.current_page &&
            activities.value
          ) {
            activities.value = activities.value.concat(events);
          } else {
            activities.value = events.concat(activities.value as IEvent[]);
          }

          callback(pageNum);
        });

        // if (events[pageNum].meta.current > currentPage) {
        //   eventsList.value = eventsList.value.concat(events[pageNum].data);
        // } else {
        //   eventsList.value = events[pageNum].data.concat(eventsList.value);
        // }
        //
        // total.value = events[pageNum].meta.total;

        // callback(events[pageNum].meta.current);
      };

      // eslint-disable-next-line @typescript-eslint/no-empty-function
      // loadPage(currentPage, function (_) {});

      const lazyLoadOptions = ref(new LazyLoadValue(0, 0));

      const localDate = new Date().toLocaleDateString();

      // методы для фильтров online/offline
      const filterOnline: Ref<boolean> = ref(false);
      const filterOffline: Ref<boolean> = ref(false);

      const selectOnline = () => {
        filterOnline.value = !filterOnline.value;

        if (
          (filterOffline.value && filterOnline.value) ||
          (!filterOffline.value && !filterOnline.value)
        ) {
          isOnline.value = null;
        } else {
          isOnline.value = filterOnline.value;
        }

        getCheckedTypeEvents();
      };

      const selectOffline = () => {
        filterOffline.value = !filterOffline.value;

        if (
          (filterOffline.value && filterOnline.value) ||
          (!filterOffline.value && !filterOnline.value)
        ) {
          isOnline.value = null;
        } else {
          isOnline.value = !filterOffline.value;
        }

        getCheckedTypeEvents();
      };

      const selectAll = () => {
        if (filterOffline.value && filterOnline.value) {
          filterOffline.value = false;
          filterOnline.value = false;
        } else {
          filterOffline.value = true;
          filterOnline.value = true;
        }

        isOnline.value = null;
        getCheckedTypeEvents();
      };

      useFetch(async () => {
        await getCheckedTypeEvents();
      });

      return {
        addCheckedType,
        activities,
        checkedTypes,
        currentEvent,
        deleteAll,
        events,
        eventsList,
        eventsOfMonth,
        lazyLoadOptions,
        loadPage,
        list,
        colorRounds,
        localDate,
        filterOnline,
        filterOffline,
        selectOnline,
        selectOffline,
        selectAll,
        typesList,
      };
    },
  });
</script>

<style lang="scss" scoped>
  @import './css/settings';
  @import './css/particles/paragraph';

  .boldText {
    font-weight: bold;
  }

  .events {
    &__menu {
      display: flex;
      gap: map-get($units, xsmall) * 18;
      padding-bottom: map-get($units, xsmall) * 15;
      flex-flow: wrap;

      &-text {
        color: $white-color;
        font-size: map-get($units, xsmall) * 14;
        line-height: map-get($units, xsmall) * 17;
        text-decoration: underline;
        cursor: pointer;
        align-self: center;
      }

      &-icon {
        align-self: center;
      }

      &-reset {
        display: flex;
        gap: map-get($units, xsmall) * 5;
      }
    }

    &__select {
      display: flex;
      align-items: center;
      height: map-get($units, xsmall) * 30;

      &-text {
        color: $white-color;
        font-size: map-get($units, xsmall) * 14;
        line-height: map-get($units, xsmall) * 17;
        padding-right: map-get($units, xsmall) * 10;
      }

      &-icon {
        align-self: center;
        padding-right: map-get($units, xsmall) * 5;
      }
    }

    &__network {
      padding-top: map-get($units, xsmall) * 16;
      padding-bottom: map-get($units, xsmall) * 30;

      &-online {
        display: flex;
        grid-column-gap: map-get($units, xsmall) * 5;
        cursor: pointer;
      }

      &-offline {
        display: flex;
        grid-column-gap: map-get($units, xsmall) * 5;
        cursor: pointer;
      }

      &-all {
        display: flex;
        grid-column-gap: map-get($units, xsmall) * 5;
        cursor: pointer;
      }

      &-text {
        align-self: center;
        font-weight: 400;
        font-family: 'Montserrat', sans-serif;
        font-size: map-get($units, xsmall) * 12;
        line-height: map-get($units, xsmall) * 15;
        color: #1d2745;
        padding-top: map-get($units, xsmall) * 10;
        padding-bottom: map-get($units, xsmall) * 13;
        border-top: map-get($units, xsmall) * 2 solid $white-color;
      }

      &-date {
        border: map-get($units, xsmall) * 1 solid $white-color;
        width: fit-content;
        font-weight: 400;
        font-family: 'Montserrat', sans-serif;
        font-size: map-get($units, xsmall) * 14;
        line-height: map-get($units, xsmall) * 17;
        border-radius: map-get($units, xsmall) * 70;
        color: $white-color;
        padding: map-get($units, xsmall) * 10 map-get($units, xsmall) * 40;
        margin-top: map-get($units, xsmall) * 20;
        margin-bottom: map-get($units, xsmall) * 50;
      }
    }
  }

  .filters {
    padding-bottom: map-get($units, xsmall) * 60;

    &__block {
      height: map-get($units, xsmall) * 23;
      width: map-get($units, xsmall) * 23;
      border: map-get($units, xsmall) * 1 solid $white-color;
      border-radius: 50%;
      display: flex;
      justify-content: center;
      align-items: center;
      overflow: hidden;
    }

    &__checkbox {
      display: flex;
      gap: map-get($units, xsmall) * 20;

      &-input {
        height: map-get($units, xsmall) * 10;
        width: map-get($units, xsmall) * 10;
        -webkit-appearance: none;
        -moz-appearance: none;
        appearance: none;
        border-radius: 50%;
        outline: none;
        transition-duration: 0.3s;
        cursor: pointer;

        &:checked {
          height: map-get($units, xsmall) * 23;
          width: map-get($units, xsmall) * 23;
        }
      }

      &-text {
        color: $white-color;
        cursor: pointer;
        font-size: map-get($units, xsmall) * 14;
        line-height: map-get($units, xsmall) * 17;
        padding-bottom: map-get($units, xsmall) * 25;
        width: 80%;
      }
    }
  }

  .active {
    border-top: map-get($units, xsmall) * 2 solid $secondary-color;
  }

  .button {
    &__up {
      display: flex;
      justify-content: center;
      padding-bottom: map-get($units, xsmall) * 60;
    }

    &__down {
      display: flex;
      justify-content: center;
      padding-bottom: map-get($units, xsmall) * 60;
      padding-top: map-get($units, xsmall) * 60;
    }
  }

  .network {
    display: flex;
    border-radius: map-get($units, xsmall) * 50;
    background-color: $white-color;
    grid-column-gap: map-get($units, xsmall) * 25;
    padding: map-get($units, xsmall) * 0 map-get($units, xsmall) * 20;
    width: fit-content;
  }

  @include breakpoint(small) {
    .events {
      display: flex;

      &__menu {
        gap: map-get($units, small) * 18;
        padding-bottom: initial;
        padding-right: map-get($units, small) * 48;

        &-text {
          font-size: map-get($units, small) * 14;
          line-height: map-get($units, small) * 17;
        }

        &-reset {
          gap: map-get($units, small) * 5;
        }
      }

      &__select {
        height: map-get($units, small) * 30;

        &-text {
          font-size: map-get($units, small) * 14;
          line-height: map-get($units, small) * 17;
          padding-right: map-get($units, small) * 10;
        }

        &-icon {
          padding-right: map-get($units, small) * 5;
        }
      }

      &__network {
        display: flex;
        padding-top: map-get($units, small) * 30;
        padding-bottom: map-get($units, small) * 50;
        gap: map-get($units, small) * 40;

        &-online {
          grid-column-gap: map-get($units, small) * 5;
        }

        &-offline {
          grid-column-gap: map-get($units, small) * 5;
        }

        &-all {
          grid-column-gap: map-get($units, small) * 5;
        }

        &-text {
          font-size: map-get($units, small) * 12;
          line-height: map-get($units, small) * 15;
          padding-top: map-get($units, small) * 13;
          padding-bottom: map-get($units, small) * 16;
          border-top: map-get($units, small) * 2 solid $white-color;
        }

        &-date {
          align-self: center;
          border-width: map-get($units, small) * 1;
          border-radius: map-get($units, small) * 70;
          font-size: map-get($units, small) * 14;
          line-height: map-get($units, small) * 17;
          padding: map-get($units, small) * 13 map-get($units, small) * 40;
          margin-top: initial;
          margin-bottom: initial;
        }
      }
    }

    .filters {
      padding-bottom: map-get($units, small) * 60;

      &__block {
        height: map-get($units, small) * 23;
        width: map-get($units, small) * 23;
        border-width: map-get($units, small) * 1;
      }

      &__checkbox {
        gap: map-get($units, small) * 20;

        &-input {
          height: map-get($units, small) * 10;
          width: map-get($units, small) * 10;
          border-width: map-get($units, small) * 1;

          &:checked {
            height: map-get($units, small) * 23;
            width: map-get($units, small) * 23;
          }
        }

        &-text {
          font-size: map-get($units, small) * 14;
          line-height: map-get($units, small) * 17;
          padding-bottom: map-get($units, small) * 30;
        }
      }
    }

    .active {
      border-top: map-get($units, small) * 2 solid $secondary-color;
    }

    .button {
      &__up {
        padding-bottom: map-get($units, small) * 60;
      }

      &__down {
        padding-bottom: map-get($units, small) * 60;
        padding-top: map-get($units, small) * 60;
      }
    }

    .network {
      display: flex;
      border-radius: map-get($units, small) * 50;
      grid-column-gap: map-get($units, small) * 25;
      padding: map-get($units, small) * 0 map-get($units, small) * 20;
    }
  }

  @include breakpoint(medium) {
    .events {
      &__menu {
        gap: map-get($units, medium) * 18;
        padding-right: map-get($units, medium) * 48;

        &-text {
          font-size: map-get($units, medium) * 14;
          line-height: map-get($units, medium) * 17;
        }

        &-reset {
          gap: map-get($units, medium) * 5;
        }
      }

      &__select {
        height: map-get($units, medium) * 30;

        &-text {
          font-size: map-get($units, medium) * 14;
          line-height: map-get($units, medium) * 17;
          padding-right: map-get($units, medium) * 10;
        }

        &-icon {
          padding-right: map-get($units, medium) * 5;
        }
      }

      &__network {
        padding-top: map-get($units, medium) * 20;
        padding-bottom: map-get($units, medium) * 40;
        gap: map-get($units, medium) * 40;

        &-online {
          grid-column-gap: map-get($units, medium) * 5;
        }

        &-offline {
          grid-column-gap: map-get($units, medium) * 5;
        }

        &-all {
          grid-column-gap: map-get($units, medium) * 5;
        }

        &-text {
          font-size: map-get($units, medium) * 12;
          line-height: map-get($units, medium) * 15;
          padding-top: map-get($units, medium) * 13;
          padding-bottom: map-get($units, medium) * 16;
          border-top: map-get($units, medium) * 2 solid $white-color;
        }

        &-date {
          border-width: map-get($units, medium) * 1;
          border-radius: map-get($units, medium) * 70;
          font-size: map-get($units, medium) * 14;
          line-height: map-get($units, medium) * 17;
          padding: map-get($units, medium) * 13 map-get($units, medium) * 40;
        }
      }
    }

    .filters {
      padding-bottom: map-get($units, medium) * 60;

      &__block {
        height: map-get($units, medium) * 23;
        width: map-get($units, medium) * 23;
        border-width: map-get($units, medium) * 1;
      }

      &__checkbox {
        gap: map-get($units, medium) * 20;

        &-input {
          height: map-get($units, medium) * 10;
          width: map-get($units, medium) * 10;
          border-width: map-get($units, medium) * 1;

          &:checked {
            height: map-get($units, medium) * 23;
            width: map-get($units, medium) * 23;
          }
        }

        &-text {
          font-size: map-get($units, medium) * 14;
          line-height: map-get($units, medium) * 17;
          padding-bottom: map-get($units, medium) * 30;
        }
      }
    }

    .active {
      border-top: map-get($units, medium) * 2 solid $secondary-color;
    }

    .button {
      &__up {
        padding-bottom: map-get($units, medium) * 60;
      }

      &__down {
        padding-bottom: map-get($units, medium) * 60;
        padding-top: map-get($units, medium) * 60;
      }
    }

    .network {
      border-radius: map-get($units, medium) * 50;
      grid-column-gap: map-get($units, medium) * 25;
      padding: map-get($units, medium) * 0 map-get($units, medium) * 20;
    }
  }

  @include breakpoint(large) {
    .filter {
      display: grid;
      grid-template-columns: 55% auto;
      padding-bottom: map-get($units, large) * 50;
    }
    .events {
      &__menu {
        gap: map-get($units, large) * 18;
        padding-right: map-get($units, large) * 48;

        &-text {
          font-size: map-get($units, large) * 14;
          line-height: map-get($units, large) * 17;
          align-self: center;
        }

        &-reset {
          gap: map-get($units, large) * 5;
        }
      }

      &__select {
        height: initial;

        &-text {
          font-size: map-get($units, large) * 14;
          line-height: map-get($units, large) * 17;
          padding-right: map-get($units, large) * 10;
          align-self: center;
        }

        &-icon {
          padding-right: map-get($units, large) * 5;
        }
      }

      &__network {
        padding-top: initial;
        padding-bottom: initial;
        display: flex;
        justify-content: flex-end;

        &-online {
          grid-column-gap: map-get($units, large) * 5;
        }

        &-offline {
          grid-column-gap: map-get($units, large) * 5;
        }

        &-all {
          grid-column-gap: map-get($units, large) * 5;
        }

        &-text {
          font-size: map-get($units, large) * 12;
          line-height: map-get($units, large) * 15;
          padding-top: map-get($units, large) * 13;
          padding-bottom: map-get($units, large) * 16;
          border-top: map-get($units, large) * 2 solid $white-color;
        }

        &-date {
          border-width: map-get($units, large) * 1;
          border-radius: map-get($units, large) * 70;
          font-size: map-get($units, large) * 14;
          line-height: map-get($units, large) * 17;
          padding: map-get($units, large) * 13 map-get($units, large) * 40;
        }
      }
    }

    .filters {
      display: grid;
      grid-template-columns: 52% 35%;
      justify-content: space-between;
      padding-bottom: map-get($units, large) * 60;

      &__block {
        height: map-get($units, large) * 23;
        width: map-get($units, large) * 23;
        border-width: map-get($units, large) * 1;
      }

      &__checkbox {
        gap: map-get($units, large) * 20;

        &-input {
          height: map-get($units, large) * 10;
          width: map-get($units, large) * 10;
          border-width: map-get($units, large) * 1;

          &:checked {
            height: map-get($units, large) * 23;
            width: map-get($units, large) * 23;
          }
        }

        &-text {
          font-size: map-get($units, large) * 14;
          line-height: map-get($units, large) * 17;
          padding-bottom: map-get($units, large) * 30;
        }
      }
    }

    .active {
      border-top: map-get($units, large) * 2 solid $secondary-color;
    }

    .button {
      &__up {
        padding-bottom: map-get($units, large) * 60;
      }

      &__down {
        padding-bottom: map-get($units, large) * 60;
        padding-top: map-get($units, large) * 60;
      }
    }

    .network {
      border-radius: map-get($units, large) * 50;
      grid-column-gap: map-get($units, large) * 25;
      padding: map-get($units, large) * 0 map-get($units, large) * 20;
    }
  }

  @include breakpoint(xlarge) {
    .filter {
      grid-column-gap: map-get($units, xlarge) * 75;
      padding-bottom: map-get($units, xlarge) * 60;
    }
    .events {
      &__menu {
        gap: map-get($units, xlarge) * 18;
        padding-right: map-get($units, xlarge) * 48;

        &-text {
          font-size: map-get($units, xlarge) * 14;
          line-height: map-get($units, xlarge) * 17;
        }

        &-reset {
          gap: map-get($units, xlarge) * 5;
        }
      }

      &__select {
        &-text {
          font-size: map-get($units, xlarge) * 14;
          line-height: map-get($units, xlarge) * 17;
          padding-right: map-get($units, xlarge) * 10;
        }

        &-icon {
          padding-right: map-get($units, xlarge) * 5;
        }
      }

      &__network {
        gap: map-get($units, xlarge) * 40;

        &-online {
          grid-column-gap: map-get($units, xlarge) * 5;
        }

        &-offline {
          grid-column-gap: map-get($units, xlarge) * 5;
        }

        &-all {
          grid-column-gap: map-get($units, xlarge) * 5;
        }

        &-text {
          font-size: map-get($units, xlarge) * 12;
          line-height: map-get($units, xlarge) * 15;
          padding-top: map-get($units, xlarge) * 13;
          padding-bottom: map-get($units, xlarge) * 16;
          border-top: map-get($units, xlarge) * 2 solid $white-color;
        }

        &-date {
          border-width: map-get($units, xlarge) * 1;
          border-radius: map-get($units, xlarge) * 70;
          font-size: map-get($units, xlarge) * 14;
          line-height: map-get($units, xlarge) * 17;
          padding: map-get($units, xlarge) * 13 map-get($units, xlarge) * 40;
        }
      }
    }

    .filters {
      grid-template-columns: 29% 29% 29%;
      padding-bottom: map-get($units, xlarge) * 60;

      &__block {
        height: map-get($units, xlarge) * 23;
        width: map-get($units, xlarge) * 23;
        border-width: map-get($units, xlarge) * 1;
      }

      &__checkbox {
        gap: map-get($units, xlarge) * 20;

        &-input {
          height: map-get($units, xlarge) * 10;
          width: map-get($units, xlarge) * 10;
          border-width: map-get($units, xlarge) * 1;

          &:checked {
            height: map-get($units, xlarge) * 23;
            width: map-get($units, xlarge) * 23;
          }
        }

        &-text {
          font-size: map-get($units, xlarge) * 14;
          line-height: map-get($units, xlarge) * 17;
          padding-bottom: map-get($units, xlarge) * 30;
        }
      }
    }

    .active {
      border-top: map-get($units, xlarge) * 2 solid $secondary-color;
    }

    .button {
      &__up {
        padding-bottom: map-get($units, xlarge) * 60;
      }

      &__down {
        padding-bottom: map-get($units, xlarge) * 60;
        padding-top: map-get($units, xlarge) * 60;
      }
    }

    .network {
      border-radius: map-get($units, xlarge) * 50;
      grid-column-gap: map-get($units, xlarge) * 25;
      padding: map-get($units, xlarge) * 0 map-get($units, xlarge) * 20;
    }
  }

  @include breakpoint(xxlarge) {
    .filter {
      grid-column-gap: map-get($units, xxlarge) * 170;
      padding-bottom: map-get($units, xxlarge) * 60;
    }
    .events {
      &__menu {
        gap: map-get($units, xxlarge) * 18;
        padding-right: map-get($units, xxlarge) * 48;

        &-text {
          font-size: map-get($units, xxlarge) * 14;
          line-height: map-get($units, xxlarge) * 17;
        }

        &-reset {
          gap: map-get($units, xxlarge) * 5;
        }
      }

      &__select {
        &-text {
          font-size: map-get($units, xxlarge) * 14;
          line-height: map-get($units, xxlarge) * 17;
          padding-right: map-get($units, xxlarge) * 10;
        }

        &-icon {
          padding-right: map-get($units, xxlarge) * 5;
        }
      }

      &__network {
        gap: map-get($units, xxlarge) * 40;

        &-online {
          grid-column-gap: map-get($units, xxlarge) * 5;
        }

        &-offline {
          grid-column-gap: map-get($units, xxlarge) * 5;
        }

        &-all {
          grid-column-gap: map-get($units, xxlarge) * 5;
        }

        &-text {
          font-size: map-get($units, xxlarge) * 12;
          line-height: map-get($units, xxlarge) * 15;
          padding-top: map-get($units, xxlarge) * 13;
          padding-bottom: map-get($units, xxlarge) * 16;
          border-top: map-get($units, xxlarge) * 2 solid $white-color;
        }

        &-date {
          border-width: map-get($units, xxlarge) * 1;
          border-radius: map-get($units, xxlarge) * 70;
          font-size: map-get($units, xxlarge) * 14;
          line-height: map-get($units, xxlarge) * 17;
          padding: map-get($units, xxlarge) * 13 map-get($units, xxlarge) * 40;
        }
      }
    }

    .filters {
      padding-bottom: map-get($units, xxlarge) * 60;

      &__block {
        height: map-get($units, xxlarge) * 23;
        width: map-get($units, xxlarge) * 23;
        border-width: map-get($units, xxlarge) * 1;
      }

      &__checkbox {
        gap: map-get($units, xxlarge) * 20;

        &-input {
          height: map-get($units, xxlarge) * 10;
          width: map-get($units, xxlarge) * 10;
          border-width: map-get($units, xxlarge) * 1;

          &:checked {
            height: map-get($units, xxlarge) * 23;
            width: map-get($units, xxlarge) * 23;
          }
        }

        &-text {
          font-size: map-get($units, xxlarge) * 16;
          line-height: map-get($units, xxlarge) * 20;
          padding-bottom: map-get($units, xxlarge) * 30;
        }
      }
    }

    .active {
      border-top: map-get($units, xxlarge) * 2 solid $secondary-color;
    }

    .button {
      &__up {
        padding-bottom: map-get($units, xxlarge) * 60;
      }

      &__down {
        padding-bottom: map-get($units, xxlarge) * 60;
        padding-top: map-get($units, xxlarge) * 60;
      }
    }

    .network {
      border-radius: map-get($units, xxlarge) * 50;
      grid-column-gap: map-get($units, xxlarge) * 25;
      padding: map-get($units, xxlarge) * 0 map-get($units, xxlarge) * 20;
    }
  }
</style>
