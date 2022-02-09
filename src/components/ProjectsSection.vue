<template>
  <div v-if='projects.length' class='q-pa-md row items-start q-gutter-md'>
    <q-card class='my-card'>
      <q-card-section>
        <div class='text-h6'>Projects
          <q-chip ripple='false'>
            <div>Visit <a href='https://github.com/lpssss/Projects' style='text-decoration: none'
                          target='_blank'>here</a> for codes
              and reports
            </div>
          </q-chip>
        </div>
        <div class='q-pt-sm'>
          <q-list bordered class='rounded-borders' separator>
            <q-expansion-item v-for='idx in projects.length' :key='idx'>
              <q-separator />
              <template v-slot:header>
                <q-item-section avatar>
                  <q-avatar color='secondary' text-color='black'>{{ idx }}</q-avatar>
                </q-item-section>
                <q-item-section>
                  <q-item-label class='text-h6'>{{ projects[idx - 1].projectTitle }}
                    <q-icon v-if='projects[idx - 1].star' class='items-center' color='yellow' name='star' />
                  </q-item-label>
                  <q-item-label caption>{{ projects[idx - 1].caption }}</q-item-label>
                </q-item-section>
              </template>

              <q-card>
                <q-card-section>
                  <q-chip color='blue' icon='event' outline>{{ projects[idx - 1].date }}</q-chip>
                  <q-chip color='red' icon='stairs' outline>{{ projects[idx - 1].difficulty }}</q-chip>
                  <q-chip v-for='tool in projects[idx-1].techStack' :key='tool' class='text-white' color='positive'>
                    {{ tool }}
                  </q-chip>
                </q-card-section>
                <q-card-section>
                  <q-list dense>
                    <q-item v-for='line in projects[idx - 1].elaboration' :key='line'>
                      <q-item-section avatar>
                        <q-icon color='primary' name='fas fa-hand-point-right' />
                      </q-item-section>

                      <q-item-section>{{ line }}</q-item-section>
                    </q-item>
                  </q-list>

                </q-card-section>
              </q-card>
            </q-expansion-item>
          </q-list>
        </div>
      </q-card-section>
    </q-card>
  </div>
</template>

<script lang='ts'>
import { defineComponent, ref } from 'vue';
import { api } from 'boot/axios';
import { ApiLinks } from 'src/api-links';
import { AxiosResponse } from 'axios';
import { useQuasar } from 'quasar';

const API_LINK = ApiLinks.Projects;
export default defineComponent({
  name: 'ProjectsSection',
  props: {
    admin: Boolean
  },
  setup() {
    interface Projects {
      id: string;
      projectTitle: string;
      techStack: Array<string>;
      elaboration: Array<string>;
      caption: string;
      date: string;
      difficulty: string;
      star: boolean;
    }

    interface ObjectofString {
      [key: string]: number;
    }

    const projects = ref<Projects[]>([]);
    const $q=useQuasar()
    $q.loading.show({
      delay:500
    })

    function capitalizeTitle(title: string): string {
      const words = title.split(' ');
      return words.map((word) =>
        word[0].toUpperCase() + word.slice(1)
      ).join(' ');
    }

    function sortCompare(a: Projects, b: Projects) {
      const difficultyMap: ObjectofString = {
        'Advanced': 2,
        'Intermediate': 1,
        'Beginner': 0
      };
      if (a.star === b.star) {
        if (a.difficulty === b.difficulty)
          return 0;
        else if (difficultyMap[a.difficulty] > difficultyMap[b.difficulty])
          return -1;
        else return 1;
      } else if (a.star) {
        return -1;
      } else return 1;
    }

    async function getProjectsData() {
      try {
        const response: AxiosResponse<Projects[]> = await api.get(API_LINK);
        response.data.sort(sortCompare);
        response.data.forEach(item => item.projectTitle = capitalizeTitle(item.projectTitle));
        projects.value = response.data;
        $q.loading.hide()
      } catch (error) {
        console.log(error);
      }
    }

    void getProjectsData();

    return {
      projects
    };
  }

});
</script>

<style lang='scss' scoped>
.my-card {
  width: 100%
}
</style>
