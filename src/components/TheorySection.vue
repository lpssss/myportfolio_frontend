<template>
  <div v-if='Object.keys(coursesByType).length' class='q-pa-md row items-start q-gutter-md'>
    <q-card class='my-card'>
      <q-card-section>
        <div class='text-h6'>Core Courses</div>
        <div class='q-pt-sm'>
          <q-list bordered class='rounded-borders' separator>
            <q-expansion-item v-for='courseType in Object.keys(coursesByType)' :key='courseType'>
              <q-separator />
              <template v-slot:header>
                <q-item-section avatar>
                  <q-avatar color='orange' text-color='white' icon='subject' />
                </q-item-section>
                <q-item-section>
                  <q-item-label class='text-h6'>{{courseType}}</q-item-label>
                </q-item-section>
              </template>

              <q-card>
                <q-card-section>
                  <q-markup-table separator='cell'>
                    <thead>
                    <tr>
                      <th class='text-center'>Course</th>
                      <th class='text-center'>Contents</th>
                    </tr>
                    </thead>
                    <tbody>
                    <tr v-for='course in coursesByType[courseType]' :key='course.id'>
                      <td class='text-center'>{{course.courseTitle}}</td>
                      <td class='text-center'>{{course.contents}}</td>
                    </tr>
                    </tbody>
                  </q-markup-table>
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
import { AxiosResponse } from 'axios';
import { api } from 'boot/axios';
import { ApiLinks } from 'src/api-links';
import { defineComponent, reactive } from 'vue';

const API_LINK=ApiLinks.Courses

export default defineComponent({
  name: 'TheorySection',
  setup() {
    interface Courses {
      id: string;
      courseTitle:string;
      contents:string;
      courseType:string
    }
    interface CoursesByType{
      [key:string]:Array<Courses>;
    }

    const coursesByType=reactive<CoursesByType>({})

    function classifyCourses(data:Courses[]):void{
      data.forEach(item=>{
        if(item.courseType in coursesByType) {
          coursesByType[item.courseType].push(item)
        }
        else{
          coursesByType[item.courseType]=[item]
        }
      })
      console.log(coursesByType)
    }

    async function getCoursesData() {
      try {
        const response: AxiosResponse<Courses[]> = await api.get(API_LINK);
        console.log(response.data)
        classifyCourses(response.data)
      } catch (error) {
        console.log(error);
      }
    }

    void getCoursesData();

    return {
      coursesByType
    };
  }
});
</script>

<style lang='scss' scoped>
.my-card {
  width: 100%
}
</style>
