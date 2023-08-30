<template>
  <div v-if="visible" class="w-full p-20">
    <div class="bg-white rounded-xl shadow-sm h-auto relative">
      <button
        type="button"
        class="py-2 px-4 bg-gray-200 rounded-md absolute bottom-5 right-5"
        @click="visible = false"
      >
        close
      </button>

      <div v-if="country" class="p-10">
        <div class="flex flex-row gap-x-4 mb-12">
          <img :src="country?.flags?.png" class="rounded-md h-32" />
          <div class="p-2">
            <div class="text-3xl mb-3">{{ country?.name?.common }}</div>
            <div class="text-xl">{{ country?.name?.official }}</div>
          </div>
        </div>

        <div
          class="flex flex-col gap-y-2 overflow-y-auto h-[55vh] mb-6 divide-y border-t"
        >
          <div class="grid grid-cols-1 gap-y-2 py-2">
            <div class="flex gap-2">
              <label
                class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
              >
                Native Name
              </label>
              <div class="flex flex-row" v-if="country?.name?.nativeName">
                <div
                  v-for="(nativeNameKey, index) in Object.keys(
                    country?.name?.nativeName
                  )"
                >
                  <label>
                    {{ nativeNameKey }}
                  </label>
                  <div class="flex">
                    <di class="grid grid-cols-1 gap-2 ml-10">
                      <li class="list-disc">
                        Official
                        {{
                          Object.values(country?.name?.nativeName)[index]
                            .official
                        }},
                      </li>
                      <li class="list-disc">
                        Common
                        {{
                          Object.values(country?.name?.nativeName)[index].common
                        }}
                      </li>
                    </di>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <div v-for="tld in country?.tld" class="py-2">
            <label
              class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
            >
              TLD
            </label>
            {{ tld }}
          </div>
          <div class="py-2">
            <label
              class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
            >
              CCA2
            </label>
            {{ country?.cca2 }}
          </div>
          <div class="py-2">
            <label
              class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
            >
              CCN3
            </label>
            {{ country?.ccn3 }}
          </div>
          <div class="py-2">
            <label
              class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
            >
              CCA3
            </label>
            {{ country?.cca3 }}
          </div>
          <div class="py-2">
            <label
              class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
            >
              CIOC
            </label>
            {{ country?.cioc }}
          </div>
          <div class="py-2">
            <label
              class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
            >
              Independent
            </label>
            {{ country?.independent }}
          </div>
          <div class="py-2">
            <label
              class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
            >
              Status
            </label>
            {{ country?.status }}
          </div>
          <div class="py-2">
            <label
              class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
            >
              UN Member
            </label>
            {{ country?.unMember }}
          </div>
          <div class="py-2">
            <label
              class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
            >
              Region
            </label>
            {{ country?.region }}
          </div>
          <div class="py-2">
            <label
              class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
            >
              Subregion
            </label>
            {{ country?.subregion }}
          </div>
          <div class="py-2">
            <label
              class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
            >
              Latitude Longitude
            </label>
            {{ country?.latlng[0] + ", " + country?.latlng[1] }}
          </div>
          <div class="py-2">
            <label
              class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
            >
              Land Locked
            </label>
            {{ country?.landlocked }}
          </div>
          <div class="py-2">
            <label
              class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
            >
              Area
            </label>
            {{ country?.area }}
          </div>
          <div class="py-2">
            <label
              class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
            >
              Flag
            </label>
            {{ country?.flag }}
          </div>
          <div class="py-2">
            <label
              class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
            >
              Population
            </label>
            {{ country?.population }}
          </div>
          <div class="py-2">
            <label
              class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
            >
              Fifa
            </label>

            <span v-if="country?.fifa">{{ country?.fifa }}</span>
            <span v-else> N/A </span>
          </div>
          <div class="py-2">
            <label
              class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
            >
              Start Of Week
            </label>
            {{ country?.startOfWeek }}
          </div>

          <div class="grid grid-cols-1 gap-y-2 py-2">
            <div class="flex gap-2">
              <label
                class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
              >
                Capital Info
              </label>
              <div>
                <span>
                  {{
                    country?.capitalInfo?.latlng?.[0] +
                    ", " +
                    country?.capitalInfo?.latlng?.[1]
                  }}
                </span>
              </div>
            </div>
          </div>

          <div class="grid grid-cols-1 gap-y-2 py-2">
            <div class="flex gap-2">
              <label
                class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
              >
                Currencies
              </label>
              <div v-if="country?.currencies">
                <div
                  v-for="(currency, index) in Object.keys(country?.currencies)"
                >
                  <span> {{ currency }}</span>
                  <div class="flex">
                    <ul class="grid grid-cols-1 gap-2 ml-10">
                      <li class="list-disc">
                        Name
                        {{ Object.values(country?.currencies)[index].name }},
                      </li>
                      <li class="list-disc">
                        Symbol
                        {{ Object.values(country?.currencies)[index].symbol }}
                      </li>
                    </ul>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <div class="grid grid-cols-1 gap-y-2 py-2">
            <div class="flex gap-2">
              <label
                class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
              >
                Capital
              </label>
              <div>
                <div class="flex flex-wrap">
                  <span v-for="capital in country?.capital">
                    {{ capital }}
                  </span>
                </div>
              </div>
            </div>
          </div>

          <div class="grid grid-cols-1 gap-y-2 py-2">
            <div class="flex gap-2">
              <label
                class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
              >
                Alt Spellings
              </label>
              <div>
                <div class="flex flex-wrap">
                  <span v-for="(altSpelling, index) in country?.altSpellings">
                    {{ altSpelling }}
                    <span v-if="country?.altSpellings?.length > index + 1">
                      ,
                    </span>
                  </span>
                </div>
              </div>
            </div>
          </div>

          <div class="grid grid-cols-1 gap-y-2 py-2">
            <div class="flex gap-2">
              <label
                class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
              >
                Borders
              </label>
              <div>
                <div v-if="country?.borders" class="flex flex-wrap">
                  <span v-for="(border, index) in country?.borders">
                    {{ border }}
                    <span v-if="country?.borders?.length > index + 1"> , </span>
                  </span>
                </div>
                <span> N/A </span>
              </div>
            </div>
          </div>

          <div class="grid grid-cols-1 gap-y-2 py-2">
            <div class="flex gap-2">
              <label
                class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
              >
                Demonyms
              </label>
              <div v-if="country?.demonyms">
                <div v-for="(demonym, index) in Object.keys(country?.demonyms)">
                  <span> {{ demonym }}</span>
                  <div class="flex">
                    <ul class="grid grid-cols-1 gap-2 ml-10">
                      <li class="list-disc">
                        F
                        {{ Object.values(country?.demonyms)[index].f }},
                      </li>
                      <li class="list-disc">
                        M
                        {{ Object.values(country?.demonyms)[index].m }}
                      </li>
                    </ul>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <div class="grid grid-cols-1 gap-y-2 py-2">
            <div class="flex gap-2">
              <label
                class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
              >
                Maps
              </label>
              <div class="grid grid-cols-1 gap-2">
                <div>
                  <label>Google Maps</label>
                  <a
                    :href="country?.maps?.googleMaps"
                    target="_blank"
                    class="text-blue-400"
                  >
                    {{ country?.maps?.googleMaps }}
                  </a>
                </div>
                <div>
                  <label>Open Street Maps </label>
                  <a
                    :href="country?.maps?.openStreetMaps"
                    target="_blank"
                    class="text-blue-400"
                  >
                    {{ country?.maps?.openStreetMaps }}
                  </a>
                </div>
              </div>
            </div>
          </div>

          <div class="grid grid-cols-1 gap-y-2 py-2">
            <div class="flex gap-2">
              <label
                class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
              >
                Car
              </label>
              <div class="grid grid-cols-1 gap-2">
                <div>
                  <div class="flex flex-wrap">
                    <label class="mr-1">Signs</label>
                    <span v-for="(sign, index) in country?.car?.signs">
                      {{ sign }}
                      <span v-if="country?.car?.signs?.length > index + 1">
                        ,
                      </span>
                    </span>
                  </div>
                </div>
                <div>Side {{ country?.car?.side }}</div>
              </div>
            </div>
          </div>

          <div class="grid grid-cols-1 gap-y-2 py-2">
            <div class="flex gap-2">
              <label
                class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
              >
                Timezones
              </label>
              <div>
                <div class="flex flex-wrap">
                  <span v-for="(timezone, index) in country?.timezones">
                    {{ timezone }}
                    <span v-if="country?.timezones?.length > index + 1">
                      ,
                    </span>
                  </span>
                </div>
              </div>
            </div>
          </div>

          <div class="grid grid-cols-1 gap-y-2 py-2">
            <div class="flex gap-2">
              <label
                class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
              >
                Continents
              </label>
              <div>
                <div class="flex flex-wrap">
                  <span v-for="(continent, index) in country?.continents">
                    {{ continent }}
                    <span v-if="country?.continents?.length > index + 1">
                      ,
                    </span>
                  </span>
                </div>
              </div>
            </div>
          </div>

          <div class="grid grid-cols-1 gap-y-2 py-2">
            <div class="flex gap-2">
              <label
                class="flex-none font-bold inline-block w-52 text-gray-400 uppercase text-sm"
              >
                Flags
              </label>
              <div class="flex-auto">
                <div class="grid grid-cols-1 gap-2">
                  <div class="flex flex-row items-center">
                    <label class="mr-6">Png </label>
                    <img :src="country?.flags?.png" class="h-10" />
                  </div>
                  <div class="flex flex-row items-center">
                    <label class="mr-6">Svg </label>
                    <img :src="country?.flags?.svg" class="h-10" />
                  </div>
                  <div class="flex flex-row">
                    <label class="mr-6 flex-none"> Alt </label>
                    {{ country?.flags?.alt }}
                  </div>
                </div>
              </div>
            </div>
          </div>

          <div class="grid grid-cols-1 gap-y-2 py-2">
            <div class="flex gap-2">
              <label
                class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
              >
                Coat Of Arms
              </label>
              <div class="grid grid-cols-1 gap-2">
                <div class="flex flex-row items-center">
                  <label class="mr-6">Png </label>
                  <img :src="country?.coatOfArms?.png" class="h-10" />
                </div>
                <div class="flex flex-row items-center">
                  <label class="mr-6">Svg </label>
                  <img :src="country?.coatOfArms?.svg" class="h-10" />
                </div>
              </div>
            </div>
          </div>

          <div class="grid grid-cols-1 gap-y-2 py-2">
            <div class="flex gap-2">
              <label
                class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
              >
                Postal Code
              </label>
              <div class="grid grid-cols-1 gap-2">
                <div>
                  Format
                  <span v-if="country?.postalCode?.format">
                    {{ country?.postalCode?.format }}
                  </span>
                </div>
                <div>
                  Regex
                  <span v-if="country?.postalCode?.regex">
                    {{ country?.postalCode?.regex }}
                  </span>
                </div>
              </div>
            </div>
          </div>

          <div class="grid grid-cols-1 gap-y-2 py-2">
            <div class="flex gap-2">
              <label
                class="flex-none font-bold inline-block w-52 text-gray-400 uppercase text-sm"
              >
                IDD
              </label>
              <div class="flex-auto">
                <div
                  v-if="country?.idd?.suffixes?.length > 0"
                  class="flex flex-wrap"
                >
                  <div
                    v-for="(suffix, index) in country?.idd?.suffixes"
                    class="w-28"
                  >
                    {{ country?.idd?.root + suffix }}
                    <span
                      v-if="country?.idd?.suffixes?.length > index + 1"
                      class="mr-1"
                    >
                      ,
                    </span>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <div class="grid grid-cols-1 gap-y-2 py-2">
            <div class="flex gap-2">
              <label
                class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
              >
                Languages
              </label>
              <div v-if="country?.languages">
                <div
                  v-for="(language, index) in Object.keys(country?.languages)"
                >
                  <span> {{ language }}</span>
                  <div class="flex">
                    <ul class="grid grid-cols-1 gap-2 ml-10">
                      <li class="list-disc">
                        {{ Object.values(country?.languages)[index] }},
                      </li>
                    </ul>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <div class="grid grid-cols-1 gap-y-2 py-2">
            <div class="flex gap-2">
              <label
                class="font-bold inline-block w-52 text-gray-400 uppercase text-sm"
              >
                Translations
              </label>
              <div v-if="country?.translations">
                <div
                  v-for="(translation, index) in Object.keys(
                    country?.translations
                  )"
                >
                  <span> {{ translation }}</span>
                  <div class="flex">
                    <ul class="grid grid-cols-1 gap-2 ml-10">
                      <li class="list-disc">
                        Official
                        {{
                          Object.values(country?.translations)[index].official
                        }},
                      </li>
                      <li class="list-disc">
                        Common
                        {{ Object.values(country?.translations)[index].common }}
                      </li>
                    </ul>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  country: {
    type: Object,
    required: true,
  },
  visible: {
    type: Object,
    default: false,
  },
});
</script>
