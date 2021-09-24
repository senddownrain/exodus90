<template>
  <v-container>
    <v-row>
      <v-col>
        <v-card>
          <v-card-title> Дни </v-card-title>
          <v-list>
            <v-list-item-group color="primary">
              <v-list-item v-for="(item, i) in days" :key="i">
                <v-list-item-content @click="showDay(item)">
                  <v-list-item-title>
                    {{ item.number }} - {{ item.title }}
                  </v-list-item-title>
                </v-list-item-content>
              </v-list-item>
            </v-list-item-group>
          </v-list>
        </v-card>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <v-card>
          <v-card-title> Недели </v-card-title>

          <v-list>
            <v-list-item-group color="primary">
              <v-list-item v-for="(item, i) in weeks" :key="i">
                <v-list-item-content @click="showWeek(item)">
                  <v-list-item-title>
                    Неделя {{ item.number }}
                  </v-list-item-title>
                </v-list-item-content>
              </v-list-item>
            </v-list-item-group>
          </v-list>
        </v-card>
      </v-col>
    </v-row>


    <!-- Диалоги для дня и недели -->
    <v-dialog
      fullscreen
      hide-overlay
      transition="dialog-bottom-transition"
      v-model="dayDialog"
    >
      <v-card>
        <v-toolbar dark color="primary">
          <v-toolbar-title>{{ currentDay.name }}</v-toolbar-title>
          <v-spacer></v-spacer>
          <v-toolbar-items>
            <v-btn icon dark @click="dayDialog = false">
              <v-icon>mdi-close</v-icon>
            </v-btn>
          </v-toolbar-items>
        </v-toolbar>
        <v-container>
          <v-row>
            <v-col>
              <p>
                <b>Номер</b>
                {{ currentDay.number }}
              </p>
              <p>
                <b>Название</b>
                {{ currentDay.title }}
              </p>

              <p>
                <b>Писание Исход {{ currentDay.verse }}</b>
                {{ currentDay.verseText }}
              </p>
              <p>
                <b>Комментарий</b>
                {{ currentDay.comment }}
              </p>
              <p>
                <b>Упражнения</b>
                {{ currentDay.exercises }}
              </p>
            </v-col>
          </v-row>
        </v-container>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="green darken-1" text @click="dayDialog = false">
            Закрыть
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>

    <v-dialog
      fullscreen
      hide-overlay
      transition="dialog-bottom-transition"
      v-model="weekDialog"
    >
      <v-card>
        <v-toolbar dark color="primary">
          <v-toolbar-title> Неделя {{ currentWeek.number }}</v-toolbar-title>
          <v-spacer></v-spacer>
          <v-toolbar-items>
            <v-btn icon dark @click="weekDialog = false">
              <v-icon>mdi-close</v-icon>
            </v-btn>
          </v-toolbar-items>
        </v-toolbar>
        <v-container>
          <v-row>
            <v-col>
              <p>
                <b>Номер</b>
                {{ currentWeek.number }}
              </p>
              <p>
                <b>Задания</b>
                {{ currentWeek.todos }}
              </p>

            </v-col>
          </v-row>
        </v-container>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="green darken-1" text @click="dayDialog = false">
            Закрыть
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-container>
</template>

<script>
import { mapGetters, mapActions } from "vuex";
export default {
  name: "ListPage",
  data() {
    return {
      dayDialog: false,
      weekDialog: false,
      currentDay: {},
      currentWeek: {},
    };
  },
  computed: {
    ...mapGetters(["weeks", "days", "settings"])
  },
  methods: {
    ...mapActions(["LOAD", "PRELOAD"]),
    update() {
      this.LOAD();
    },
    showDay(day) {
      this.currentDay = day;
      this.dayDialog = true;
    },
    showWeek(week) {
      this.currentWeek = week;
      this.weekDialog = true;
    },
  },
  created() {
    this.PRELOAD();
  },
};
</script>
