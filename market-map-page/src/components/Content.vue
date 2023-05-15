<script setup>
import { ref, reactive, computed, onMounted } from "vue";

const selectedCity = ref("Москва"); // Изначально выбрана Москва

const cities = reactive([
  {
    name: "Москве",
    isActive: true,
    addresses: [
      {
        metro: "м. Бульвар Дмитрия Донского",
        address:
          "119048, г. Москва, Комсомольский проспект, д. 42, стр. 1, помещение 1, комната 2",
        tel: "+7 895 658 56 58",
        time: {
          from: "00:08",
          by: "21:00",
        },
      },
      {
        metro: "Котельники",
        address: "Россия, Москва, Фортунатовская улица, 31/35",
        tel: "+7 895 658 56 58",
        time: {
          from: "00:08",
          by: "21:00",
        },
      },
      {
        metro: "Чертовская",
        address: "Россия, Москва, Симферопольский бульвар, 29к3",
        tel: "",
        time: {
          from: "00:08",
          by: "21:00",
        },
      },
      // Другие адреса Москвы...
    ],
  },
  {
    name: "Нижнем Новгороде",
    isActive: false,
    addresses: [
      {
        metro: "Котельники",
        address: "Россия, Москва, Фортунатовская улица, 31/35",
        tel: "+7 895 658 56 58",
        time: {
          from: "00:08",
          by: "21:00",
        },
      },
      {
        metro: "м. Бульвар Дмитрия Донского",
        address:
          "119048, г. Москва, Комсомольский проспект, д. 42, стр. 1, помещение 1, комната 2",
        tel: "+7 895 658 56 58",
        time: {
          from: "00:08",
          by: "21:00",
        },
      },
      {
        metro: "Чертовская",
        address: "Россия, Москва, Симферопольский бульвар, 29к3",
        tel: "",
        time: {
          from: "00:08",
          by: "21:00",
        },
      },
      // Другие адреса Нижнего Новгорода...
    ],
  },
  {
    name: "Красноярске",
    isActive: false,
    addresses: [
      {
        metro: "Чертовская",
        address: "Россия, Москва, Симферопольский бульвар, 29к3",
        tel: "",
        time: {
          from: "00:08",
          by: "21:00",
        },
      },
      {
        metro: "Котельники",
        address: "Россия, Москва, Фортунатовская улица, 31/35",
        tel: "+7 895 658 56 58",
        time: {
          from: "00:08",
          by: "21:00",
        },
      },
      {
        metro: "м. Бульвар Дмитрия Донского",
        address:
          "119048, г. Москва, Комсомольский проспект, д. 42, стр. 1, помещение 1, комната 2",
        tel: "+7 895 658 56 58",
        time: {
          from: "00:08",
          by: "21:00",
        },
      },
      // Другие адреса Красноярска...
    ],
  },
]);

const changeCity = (city) => {
  selectedCity.value = city;
};

const currentAddresses = computed(() => {
  return (
    cities.find((city) => city.name === selectedCity.value)?.addresses || []
  );
});

const setup = () => {
  return {
    selectedCity,
    cities,
    changeCity,
    currentAddresses,
  };
};

////////////////////////////////////////////////////// временный скрипт
///////////   вы можете использовать хук onMounted для выполнения кода после монтирования компонента
onMounted(() => {
  const tabs = document.querySelectorAll("#map_content > div");
  tabs.forEach(function (tab) {
    tab.style.display = "none";
  });
  tabs[0].style.display = "block";

  const tabLinks = document.querySelectorAll("#map_tab .nav-item a");
  tabLinks.forEach(function (link) {
    link.addEventListener("click", function (event) {
      event.preventDefault();
      tabs.forEach(function (tab) {
        tab.style.display = "none";
      });

      const target = document.querySelector(this.getAttribute("href"));
      if (target) {
        target.style.display = "block";
      }

      tabLinks.forEach(function (link) {
        link.classList.remove("active");
      });

      this.classList.add("active");
    });
  });

  tabLinks[0].click();
});
</script>

<template>
  <div id="w-node-8efe5fd4d067-ffd573ed">
    <div class="box-in">
      <div class="s-mid" id="map__content">
        <div class="inner">
          <div class="s-mid-row">
            <h2 class="title">Наши адреса</h2>
            <ul class="nav nav-tabs" id="map_tab" role="tablist">
              <li class="nav-item" v-for="city in cities" :key="city.name">
                <a
                  class="nav-link"
                  :class="{ active: selectedCity === city.name }"
                  @click="changeCity(city.name)"
                >
                  Мы в {{ city.name }}
                </a>
              </li>
            </ul>

            <div class="tab-content" id="map_content">
              <div
                class="tab-pane active in"
                id="map_msk"
                role="tabpanel"
                aria-labelledby="map_msk-tab"
              >
                <iframe
                  src="https://yandex.ru/map-widget/v1/?um=constructor%3A515f3877ea3d53273fd23d3ec4a0466559bf5d77b5fa38b9e01ce780cef2a1c5&amp;source=constructor"
                  width="100%"
                  height="400"
                  frameborder="0"
                ></iframe>
              </div>
              <div
                class="tab-pane"
                id="map_nnov"
                role="tabpanel"
                aria-labelledby="map_nnov-tab"
              >
                <iframe
                  src="https://yandex.ru/map-widget/v1/?um=constructor%3A5f4d1a068267a791df11647757dcb9bea9b0397a8f439608d526cff71b48f9ff&amp;source=constructor"
                  loading="lazy"
                  width="100%"
                  height="400"
                  frameborder="0"
                ></iframe>
              </div>
              <div
                class="tab-pane"
                id="map_kras"
                role="tabpanel"
                aria-labelledby="map_kras-tab"
              >
                <iframe
                  src="https://yandex.ru/map-widget/v1/?um=constructor%3A1e9d0ea5a75293c8639575e22954016da2c523eeb463e28f769ccca270d87ff9&amp;source=constructor"
                  width="100%"
                  height="400"
                  frameborder="0"
                ></iframe>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="box-in">
      <h3>Список наши адресов в {{ selectedCity }}</h3>

      <div class="contact_items">
        <div
          class="div-block-170 div-block-170--border"
          v-for="(address, index) in currentAddresses"
          :key="index"
        >
          <img
            src="./icons/geo.svg"
            loading="lazy"
            alt=""
            class="image-39 _1"
          />
          <div>
            <div class="h3 bold _5">{{ address.metro }}</div>
            <div>
              <p>{{ address.address }}</p>
              <a :href="'tel:' + address.tel">{{ address.tel }}</a>
              <p class="h3 bold _5">
                Ежедневно: {{ address.time.from }} - {{ address.time.by }}
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="box-in">
      <h3>Текст общий под картой и списком</h3>
    </div>

    <div class="box-in">
      <ul>
        <li>
          Процедура возврата товара регламентируется статьей 26.1 федерального
          закона «О защите прав потребителей». 
        </li>

        <li>
          Потребитель вправе отказаться от товара в любое время до его передачи,
          а после передачи товара - в течение семи дней;
        </li>

        <li>
          Возврат товара надлежащего качества возможен в случае, если сохранены
          его товарный вид, потребительские свойства, а также документ,
          подтверждающий факт и условия покупки указанного товара;
        </li>

        <li>
          Потребитель не вправе отказаться от товара надлежащего качества,
          имеющего индивидуально-определенные свойства, если указанный товар
          может быть использован исключительно приобретающим его человеком;
        </li>

        <li>
          При отказе потребителя от товара продавец должен возвратить ему
          денежную сумму, уплаченную потребителем по договору, за исключением
          расходов продавца на доставку от потребителя возвращенного товара, не
          позднее чем через десять дней со дня предъявления потребителем
          соответствующего требования;
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.div-block-170--border {
  border-bottom: 1px solid rgba(179, 179, 179, 0.3);
}
</style>
