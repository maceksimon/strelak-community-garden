<template>
  <div class="pt-4 pb-0 sm:pb-4">
    <form
      name="gardener"
      method="POST"
      data-netlify="true"
      data-netlify-honeypot="bot-field-gardener"
    >
      <div class="grid grid-cols-8 gap-6">
        <div class="relative col-span-8">
          <label for="full-name" class="block text-sm font-medium text-gray-700"
            >Jméno a příjmení <span class="text-red-700">*</span></label
          >
          <input
            v-model="formData['full-name']"
            type="text"
            name="full-name"
            id="full-name"
            autocomplete="full-name"
            class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-primary-500 focus:ring-primary-500 sm:text-sm"
            @blur="validations['full-name'].$touch"
          />
          <ErrorDisplay :validator="validations['full-name']" />
        </div>

        <div class="relative col-span-8 lg:col-span-5">
          <label
            for="email-address"
            class="block text-sm font-medium text-gray-700"
            >E-mail <span class="text-red-700">*</span></label
          >
          <input
            v-model="formData['email-address']"
            type="text"
            name="email-address"
            id="email-address"
            autocomplete="email"
            class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-primary-500 focus:ring-primary-500 sm:text-sm"
            @blur="validations['email-address'].$touch"
          />
          <ErrorDisplay :validator="validations['email-address']" />
        </div>

        <div class="relative col-span-8 lg:col-span-3">
          <label
            for="phone-number"
            class="block text-sm font-medium text-gray-700"
            >Telefon</label
          >
          <input
            v-model="formData['phone-number']"
            type="tel"
            name="phone-number"
            id="phone-number"
            autocomplete="phone-number"
            class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-primary-500 focus:ring-primary-500 sm:text-sm"
            @blur="validations['phone-number'].$touch"
          />
          <ErrorDisplay :validator="validations['phone-number']" />
        </div>

        <div class="col-span-8">
          <label for="city-part" class="block text-sm font-medium text-gray-700"
            >V jaké části Hradce bydlíte?</label
          >
          <input
            v-model="formData['city-part']"
            type="text"
            name="city-part"
            id="city-part"
            autocomplete="city-part"
            class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-primary-500 focus:ring-primary-500 sm:text-sm"
          />
        </div>

        <div class="relative col-span-8">
          <label
            for="flower-beds"
            class="block text-sm font-medium text-gray-700"
            >Kolik záhonů o rozměru 240 x 80 cm využijete?
            <span class="text-red-700">*</span></label
          >
          <select
            v-model="formData['flower-beds']"
            id="flower-beds"
            name="flower-beds"
            class="mt-1 block w-full rounded-md border border-gray-300 bg-white py-2 px-3 shadow-sm focus:border-primary-500 focus:outline-none focus:ring-primary-500 sm:text-sm"
            @blur="validations['flower-beds'].$touch"
          >
            <option :value="0.5">Půl</option>
            <option :value="1">Jeden</option>
            <option :value="1.5">Jeden a půl</option>
            <option :value="2">Dva</option>
          </select>
          <ErrorDisplay :validator="validations['flower-beds']" />
        </div>

        <div class="relative col-span-8 mb-4 space-y-4">
          <h4 class="mb-2 text-lg">
            Platba <span class="text-red-700">*</span>
          </h4>
          <div class="flex items-center">
            <input
              v-model="formData['payment-tarif']"
              id="payment-300"
              name="payment-tarif"
              type="radio"
              :value="300"
              class="h-4 w-4 border-gray-300 text-primary-600 focus:ring-primary-500"
              @blur="validations['payment-tarif'].$touch"
            />
            <label
              for="payment-300"
              class="ml-3 block text-sm font-medium text-gray-700"
            >
              Snížená - 300 Kč/sezóna
            </label>
          </div>
          <div class="flex items-center">
            <input
              v-model="formData['payment-tarif']"
              id="payment-500"
              name="payment-tarif"
              type="radio"
              :value="500"
              class="h-4 w-4 border-gray-300 text-primary-600 focus:ring-primary-500"
              @blur="validations['payment-tarif'].$touch"
            />
            <label
              for="payment-500"
              class="ml-3 block text-sm font-medium text-gray-700"
            >
              Akorát - 500 Kč/sezóna
            </label>
          </div>
          <div class="flex items-center">
            <input
              v-model="formData['payment-tarif']"
              id="payment-700"
              name="payment-tarif"
              type="radio"
              :value="700"
              class="h-4 w-4 border-gray-300 text-primary-600 focus:ring-primary-500"
              @blur="validations['payment-tarif'].$touch"
            />
            <label
              for="payment-700"
              class="ml-3 block text-sm font-medium text-gray-700"
            >
              Ideál - 700 Kč/sezóna
            </label>
          </div>
          <p class="mt-2 text-xs text-gray-500">
            Výše platby je na vás (neprokazujete se jako student/senior atp.),
            zvolte možnost podle vaší finanční situace. Údaje pro platbu pošleme
            po odeslání formuláře na váš e-mail.
          </p>
          <ErrorDisplay :validator="validations['payment-tarif']" />
        </div>

        <div class="col-span-8 flex items-start">
          <div class="flex h-5 items-center">
            <input
              v-model="formData['volunteer']"
              id="volunteer"
              name="volunteer"
              type="checkbox"
              class="h-4 w-4 rounded border-gray-300 text-primary-600 focus:ring-primary-500"
            />
          </div>
          <div class="ml-3 text-sm">
            <label for="volunteer" class="font-medium text-gray-700"
              >Dobrovolník</label
            >
            <p class="text-gray-500">
              Chci se do života zahrady zapojit také jako dobrovolník.
            </p>
          </div>
        </div>

        <div class="col-span-8 flex items-start">
          <div class="flex h-5 items-center">
            <input
              v-model="formData['newsletter']"
              id="newsletter"
              name="newsletter"
              type="checkbox"
              class="h-4 w-4 rounded border-gray-300 text-primary-600 focus:ring-primary-500"
            />
          </div>
          <div class="ml-3 text-sm">
            <label for="newsletter" class="font-medium text-gray-700"
              >Novinky</label
            >
            <p class="text-gray-500">
              Chci dostávat informace o akcích v zahradě.
            </p>
          </div>
        </div>

        <div class="col-span-8">
          <label
            for="notes-and-questions"
            class="block text-sm font-medium text-gray-700"
          >
            Prostor pro vaše poznámky či dotazy
          </label>
          <div class="mt-1">
            <textarea
              v-model="formData['notes-and-questions']"
              id="notes-and-questions"
              name="notes-and-questions"
              rows="3"
              class="block w-full rounded-md border border-gray-300 shadow-sm focus:border-primary-500 focus:ring-primary-500 sm:text-sm"
            />
          </div>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
import { computed } from "vue";
import ErrorDisplay from "./ErrorDisplay";

export default {
  components: {
    ErrorDisplay,
  },
  props: {
    modelValue: {
      type: Object,
      default: {},
    },
    validations: {
      type: Object,
      default: {},
    },
  },
  emits: ["update:modelValue", "change"],
  setup(props, { emit }) {
    const formData = computed({
      get: () => props.modelValue,
      set: (value) => {
        emit("update:modelValue", value);
        emit("change");
      },
    });

    return { formData };
  },
};
</script>
