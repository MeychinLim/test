<template>
  <div v-if="visible" class="w-full p-20">
    <div class="bg-white p-10 rounded-xl shadow-sm h-auto relative">
      <button
        type="button"
        class="py-2 px-4 bg-gray-200 rounded-md absolute bottom-4 right-4"
        @click="visible = false"
      >
        close
      </button>

      <div>
        <div class="flex flex-row gap-x-4 mb-10">
          <img :src="country?.flags?.png" class="rounded-md h-32" />
          <div class="p-2">
            <div class="text-3xl mb-3">{{ country?.name?.common }}</div>
            <div class="text-xl">{{ country?.name?.official }}</div>
          </div>
        </div>

        <div class="flex flex-col gap-y-2 overflow-y-auto h-[60vh]">
          <div class="grid grid-cols-1 gap-y-2">
            <div class="flex gap-2">
              <span> Native Name: </span>
              <div v-if="country?.name?.nativeName">
                <div
                  v-for="(nativeNameKey, index) in Object.keys(
                    country?.name?.nativeName
                  )"
                >
                  <br />
                  <span> {{ nativeNameKey + ":" }}</span>
                  <div class="flex">
                    <ul class="grid grid-cols-1 gap-2 ml-12">
                      <li class="list-disc">
                        Official:
                        {{
                          Object.values(country?.name?.nativeName)[index]
                            .official
                        }},
                      </li>
                      <li class="list-disc">
                        Common:
                        {{
                          Object.values(country?.name?.nativeName)[index].common
                        }}
                      </li>
                    </ul>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <div v-for="tld in country?.tld">TLD: {{ tld }}</div>
          <span> CCA2: {{ country?.cca2 }} </span>
          <span> CCN3: {{ country?.ccn3 }} </span>
          <span> CCA3: {{ country?.cca3 }} </span>
          <span> CIOC: {{ country?.cioc }} </span>
          <span> Independent: {{ country?.independent }} </span>
          <span> Status: {{ country?.status }} </span>
          <span> UN Member: {{ country?.unMember }} </span>

          <div class="grid grid-cols-1 gap-y-2">
            <div class="flex gap-2">
              <span> Currencies: </span>
              <div v-if="country?.currencies">
                <div
                  v-for="(currency, index) in Object.keys(country?.currencies)"
                >
                  <br />
                  <span> {{ currency + ":" }}</span>
                  <div class="flex">
                    <ul class="grid grid-cols-1 gap-2 ml-12">
                      <li class="list-disc">
                        Name:
                        {{ Object.values(country?.currencies)[index].name }},
                      </li>
                      <li class="list-disc">
                        Symbol:
                        {{ Object.values(country?.currencies)[index].symbol }}
                      </li>
                    </ul>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <div class="grid grid-cols-1 gap-y-2">
            <div class="flex gap-2">
              <span> IDD: </span>
              <div>
                <div
                  v-if="country?.idd?.suffixes?.length > 0"
                  class="flex flex-wrap"
                >
                  <span v-for="(suffix, index) in country?.idd?.suffixes">
                    {{ country?.idd?.root + suffix }}
                    <span
                      v-if="country?.idd?.suffixes?.length > index + 1"
                      class="mr-1"
                    >
                      ,
                    </span>
                  </span>
                </div>
              </div>
            </div>
          </div>

          <div class="grid grid-cols-1 gap-y-2">
            <div class="flex gap-2">
              <span> Capital: </span>
              <div>
                <div class="flex flex-wrap">
                  <span v-for="capital in country?.capital">
                    {{ capital }}
                  </span>
                </div>
              </div>
            </div>
          </div>

          <div class="grid grid-cols-1 gap-y-2">
            <div class="flex gap-2">
              <span> altSpellings: </span>
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

          <span> Region: {{ country?.region }} </span>
          <span> Subregion: {{ country?.subregion }} </span>

          <div class="grid grid-cols-1 gap-y-2">
            <div class="flex gap-2">
              <span> Languages: </span>
              <div v-if="country?.languages">
                <div
                  v-for="(language, index) in Object.keys(country?.languages)"
                >
                  <br />
                  <span> {{ language + ":" }}</span>
                  <div class="flex">
                    <ul class="grid grid-cols-1 gap-2 ml-12">
                      <li class="list-disc">
                        {{ Object.values(country?.languages)[index] }},
                      </li>
                    </ul>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <div class="grid grid-cols-1 gap-y-2">
            <div class="flex gap-2">
              <span> Translations: </span>
              <div v-if="country?.translations">
                <div
                  v-for="(translation, index) in Object.keys(
                    country?.translations
                  )"
                >
                  <br />
                  <span> {{ translation + ":" }}</span>
                  <div class="flex">
                    <ul class="grid grid-cols-1 gap-2 ml-12">
                      <li class="list-disc">
                        Official:
                        {{
                          Object.values(country?.translations)[index].official
                        }},
                      </li>
                      <li class="list-disc">
                        Common:
                        {{ Object.values(country?.translations)[index].common }}
                      </li>
                    </ul>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <span>
            Latitude Longitude:
            {{ country?.latlng[0] + ", " + country?.latlng[1] }}
          </span>
          <span> Land Locked: {{ country?.landlocked }} </span>

          <div class="grid grid-cols-1 gap-y-2">
            <div class="flex gap-2">
              <span> Borders: </span>
              <div>
                <div class="flex flex-wrap">
                  <span v-for="(border, index) in country?.borders">
                    {{ border }}
                    <span v-if="country?.borders?.length > index + 1"> , </span>
                  </span>
                </div>
              </div>
            </div>
          </div>

          <span> Area: {{ country?.area }} </span>

          <div class="grid grid-cols-1 gap-y-2">
            <div class="flex gap-2">
              <span> Demonyms: </span>
              <div v-if="country?.demonyms">
                <div v-for="(demonym, index) in Object.keys(country?.demonyms)">
                  <br />
                  <span> {{ demonym + ":" }}</span>
                  <div class="flex">
                    <ul class="grid grid-cols-1 gap-2 ml-12">
                      <li class="list-disc">
                        F:
                        {{ Object.values(country?.demonyms)[index].f }},
                      </li>
                      <li class="list-disc">
                        M:
                        {{ Object.values(country?.demonyms)[index].m }}
                      </li>
                    </ul>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <span> Flag: {{ country?.flag }} </span>

          <div class="grid grid-cols-1 gap-y-2">
            <div class="flex gap-2">
              <span> Maps: </span>
              <ul class="grid grid-cols-1 gap-2">
                <br />
                <li class="list-disc">
                  Google Maps: {{ country?.maps?.googleMaps }}
                </li>
                <li class="list-disc">
                  Open Street Maps: {{ country?.maps?.openStreetMaps }}
                </li>
              </ul>
            </div>
          </div>

          <span> Population: {{ country?.population }} </span>
          <span> Fifa: {{ country?.fifa }} </span>

          <div class="grid grid-cols-1 gap-y-2">
            <div class="flex gap-2">
              <span> Car: </span>
              <ul class="grid grid-cols-1 gap-2">
                <br />
                <li class="list-disc">
                  <div class="flex flex-wrap">
                    Signs:
                    <span v-for="(sign, index) in country?.car?.signs">
                      {{ sign }}
                      <span v-if="country?.car?.signs?.length > index + 1">
                        ,
                      </span>
                    </span>
                  </div>
                </li>
                <li class="list-disc">Side: {{ country?.car?.side }}</li>
              </ul>
            </div>
          </div>

          <div class="grid grid-cols-1 gap-y-2">
            <div class="flex gap-2">
              <span> Timezones: </span>
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

          <div class="grid grid-cols-1 gap-y-2">
            <div class="flex gap-2">
              <span> Continents: </span>
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

          <div class="grid grid-cols-1 gap-y-2">
            <div class="flex gap-2">
              <span> Flags: </span>
              <ul class="grid grid-cols-1 gap-2">
                <br />
                <li class="list-disc">
                  Png: <img :src="country?.flags?.png" class="h-10" />
                </li>
                <li class="list-disc">
                  Svg: <img :src="country?.flags?.svg" class="h-10" />
                </li>
                <li class="list-disc">Atl: {{ country?.flags?.alt }}</li>
              </ul>
            </div>
          </div>

          <div class="grid grid-cols-1 gap-y-2">
            <div class="flex gap-2">
              <span> Coat Of Arms: </span>
              <ul class="grid grid-cols-1 gap-2">
                <br />
                <li class="list-disc">
                  Png: <img :src="country?.coatOfArms?.png" class="h-10" />
                </li>
                <li class="list-disc">
                  Svg: <img :src="country?.coatOfArms?.svg" class="h-10" />
                </li>
              </ul>
            </div>
          </div>

          <span> Start Of Week: {{ country?.startOfWeek }} </span>

          <div class="grid grid-cols-1 gap-y-2">
            <div class="flex gap-2">
              <span> Capital Info: </span>
              <div>
                <span>{{
                  country?.capitalInfo?.latlng?.[0] +
                  ", " +
                  country?.capitalInfo?.latlng?.[1]
                }}</span>
              </div>
            </div>
          </div>

          <div class="grid grid-cols-1 gap-y-2">
            <div class="flex gap-2">
              <span> Postal Code: </span>
              <ul class="grid grid-cols-1 gap-2">
                <br />
                <li class="list-disc">
                  Format: {{ country?.postalCode?.format }}
                </li>
                <li class="list-disc">
                  Regex: {{ country?.postalCode?.regex }}
                </li>
              </ul>
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
