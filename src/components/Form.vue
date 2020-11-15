<template>
  <form class="form" @submit.prevent="checkForm">
    <h3>Заполните форму</h3>
    <div class="form-group">
      <label for="login">Фамилия:
      <p v-if="$v.form.lastName.$dirty && !$v.form.lastName.required" class="invalid-feedback">
        Пожалуйста, заполните поле
      </p>
      <p v-if="$v.form.lastName.$dirty && !$v.form.lastName.alpha" class="invalid-feedback">
        Не корректные данные
      </p>
      </label>
      <input
        id="lastName"
        class="form-control"
        :class="$v.form.lastName.$error ? 'is-invalid' : ''"
        v-model.trim="form.lastName"
      >
    </div>

    <div class="form-group">
      <label for="login">Имя:
      <p v-if="$v.form.firstName.$dirty && !$v.form.firstName.required" class="invalid-feedback">
        Пожалуйста, заполните поле
      </p>
      <p v-if="$v.form.firstName.$dirty && !$v.form.firstName.alpha" class="invalid-feedback">
        Не корректные данные
      </p>
      </label>
      <input
        id="firstName"
        class="form-control"
        :class="$v.form.firstName.$error ? 'is-invalid' : ''"
        v-model.trim="form.firstName"
      >
    </div>

    <div class="form-group">
      <label for="login">Отчество:
      <p v-if="$v.form.firstName.$dirty && !$v.form.patronymic.alpha" class="invalid-feedback">
        Не корректные данные
      </p>
      </label>
      <input
        id="patronymic"
        class="form-control"
        :class="$v.form.patronymic.$error ? 'is-invalid' : ''"
        v-model.trim="form.patronymic"
      >
    </div>

    <div class="form-group">
      <label for="login">Дата рождения:
      <p v-if="$v.form.date.$dirty && !$v.form.date.required" class="invalid-feedback">
        Пожалуйста, заполните поле
      </p>
      <p v-if="$v.form.date.$dirty && !$v.form.date.numeric" class="invalid-feedback">
        Не корректные данные
      </p>
      </label>
      <input
        id="date"
        class="form-control"
        :class="$v.form.date.$error ? 'is-invalid' : ''"
        v-model.trim="form.date"
      >
    </div>

     <div class="form-group">
      <label for="login">Номер телефона:
      <p v-if="$v.form.phone.$dirty && !$v.form.phone.required" class="invalid-feedback">
        Пожалуйста, заполните поле
      </p>
      <p v-if="$v.form.phone.$dirty && !$v.form.phone.numeric" class="invalid-feedback">
        Не корректные данные
      </p>
      <p v-if="$v.form.phone.$dirty && !$v.form.phone.minLength" class="invalid-feedback">
        Недостаточно цифр
      </p>
      <p v-if="$v.form.phone.$dirty && !$v.form.phone.maxLength" class="invalid-feedback">
        Слишком много цифр
      </p>
      </label>
      <input
        id="phone"
        class="form-control"
        :class="$v.form.phone.$error ? 'is-invalid' : ''"
        v-model.trim="form.phone"
      >
    </div>

    <div class="radioBtn">
      <div class="form-check">
        <input class="form-check-input" type="radio" value="male" name="exampleRadios" id="male" v-model="form.gendere" >
        <label class="form-check-label" for="male">
          Мужчина
        </label>
      </div>
      <div class="form-check">
        <input class="form-check-input" type="radio" value="female" name="exampleRadios" id="female" v-model="form.gendere">
        <label class="form-check-label" for="female">
          Женщина
        </label>
      </div>
    </div>

    <div class="form-group">
      <label for="doctors">Лечащии врач:
        <p v-if="$v.form.doctor.$dirty && !$v.form.doctor.required" class="invalid-feedback">
          Пожалуйста, выберите лечащего врача
        </p>
      </label>
      <select 
      id="doctors" 
      class="form-control" 
      :class="$v.form.phone.$error ? 'is-invalid' : ''"
      v-model="form.doctor">
        <option
         v-for="(doctor, index) in doctors"
         :value="doctor.value"
         :key="index"
        >
          {{ doctor.label }}
        </option>
      </select>
    </div>

    <div class="form-group">
      <label for="groups">Группа клиентов:
        <p v-if="$v.form.group.$dirty && !$v.form.group.required" class="invalid-feedback">
          Пожалуйста, выберите группу
        </p>
      </label>
      <select id="groups" 
        :class="$v.form.phone.$error ? 'is-invalid' : ''" 
        class="form-control" v-model="form.group" 
        multiple>
        <option
         v-for="(group, index) in groups"
         :value="group.value"
         :key="index"
        >
          {{ group.label }}
        </option>
      </select>
    </div>

    <div class="form-check">
      <input type="checkbox" id="notification" v-model="form.dontSendSms">
      <label  for="notification">Не отправлять СМС</label>
    </div>

    <div class="form-group">
      <label for="index">Индекс:</label>
      <input
        id="index"
        class="form-control"
        v-model.trim="form.index"
      >
    </div>

    <div class="form-group">
      <label for="country">Страна:</label>
      <input
        id="country"
        class="form-control"
        v-model.trim="form.country"
      >
    </div>

     <div class="form-group">
      <label for="region">Область:</label>
      <input
        id="region"
        class="form-control"
        v-model.trim="form.region"
      >
    </div>

    <div class="form-group">
      <label for="city">Город:
        <p v-if="$v.form.city.$dirty && !$v.form.city.required" class="invalid-feedback">
          Пожалуйста, заполните поле
        </p>
      </label>
      <input
        id="city"
        class="form-control"
        :class="$v.form.phone.$error ? 'is-invalid' : ''"
        v-model.trim="form.city"
      >
    </div>

    <div class="form-group">
      <label for="street">Улица:</label>
      <input
        id="street"
        class="form-control"
        v-model.trim="form.street"
      >
    </div>

    <div class="form-group">
      <label for="house">Дом:</label>
      <input
        id="house"
        class="form-control"
        v-model.trim="form.house"
      >
    </div>


    <div class="form-group">
      <label for="document">Тип документа:
        <p v-if="$v.form.document.$dirty && !$v.form.document.required" class="invalid-feedback">
          Пожалуйста, выберите тип документа
        </p>
      </label>
      <select 
      id="document" 
      class="form-control" 
      :class="$v.form.phone.$error ? 'is-invalid' : ''"
      v-model="form.document">
        <option
         v-for="(document, index) in documents"
         :value="document.value"
         :key="index"
        >
          {{ document.label }}
        </option>
      </select>
    </div>

    <div class="form-group">
      <label for="series">Серия:</label>
      <input
        id="series"
        class="form-control"
        v-model.trim="form.series"
      >
    </div>

    <div class="form-group">
      <label for="number">Номер:</label>
      <input
        id="number"
        class="form-control"
        v-model.trim="form.number"
      >
    </div>

    <div class="form-group">
      <label for="bySend">Кем выдан:</label>
      <input
        id="bySend"
        class="form-control"
        v-model.trim="form.bySend"
      >
    </div>

    <div class="form-group">
      <label for="dateOfSend">Дата выдачи:
        <p v-if="$v.form.dateOfSend.$dirty && !$v.form.dateOfSend.required" class="invalid-feedback">
          Пожалуйста, заполните поле
        </p>
      </label>
      <input
        id="dateOfSend"
        class="form-control"
        :class="$v.form.phone.$error ? 'is-invalid' : ''"
        v-model.trim="form.dateOfSend"
      >
    </div>

    <button type="submit" class="btn">Сохранить</button>

  </form>
</template>

<script>
import { validationMixin } from 'vuelidate'
import { required, minLength, maxLength, alpha, numeric, /*between, /*email */} from 'vuelidate/lib/validators'

export default {
  name: 'Form',
  mixins: [validationMixin],
  data() {
    return {
      form: {
        lastName: '',
        firstName: '',
        patronymic: '',
        date: '',
        phone: '7',
        doctor: '',
        group: [],
        dontSendSms: false,
        gendere: 'male',
        index: '',
        country: '',
        region: '',
        city: '',
        street: '',
        house: '',
        document: '',
        series: '',
        number: '',
        bySend: '',
        dateOfSend: ''
      },
      doctors: [
        {
          label: 'Иванов',
          value: 'Ivanov'
        },
        {
          label: 'Захаров',
          value: 'Zacharov'
        },
        {
          label: 'Чернышева',
          value: 'Chernysheva'
        }
      ],
      groups: [
         {
          label: 'VIP',
          value: 'VIP'
        },
        {
          label: 'Проблемные',
          value: 'problematic'
        },
        {
          label: 'ОМС',
          value: 'OMS'
        }
      ],
      documents: [
        {
          label: 'Паспорт',
          value: 'passport'
        },
        {
          label: 'Свидетельство о рождении',
          value: 'Birth certificate'
        },
        {
          label: 'Вод. удостоверение',
          value: 'license drivers'
        },
      ]
    }
  },
  validations: {
    form: {
      lastName: { required, alpha},
      firstName: { required, alpha },
      patronymic: { alpha },
      date: {required, numeric},
      phone: {required, numeric, minLength: minLength(11), maxLength: maxLength(11)},
      doctor: {required},
      group: {required},
      city: {required},
      document: {required},
      dateOfSend: {required}
    }
  },
  methods: {
    checkForm() {
      this.$v.form.$touch()
      if (!this.$v.form.$error) {
        alert('Валидация прошла успешно')
      }
    }
  }
}
</script>

<style lang="scss" scoped>

  .form-check {
    display: flex;
  }

</style>
