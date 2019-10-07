<template>
  <v-container>
    <v-layout
      wrap
    >
      <v-flex
        xs12
      >
        <v-card
          class="mx-auto my-3"
        >
          <v-card-title>1. List needs</v-card-title>
          <v-card-text>
            <p class="text-left">Derived from the stakeholders' expectations, and categorized into Value Dimensions.</p>
            <v-form 
              v-model="valid"
              ref="form"
            >
              <v-container>
                <v-row>
                  <v-col
                    cols="12"
                    md="10"
                  >
                    <v-text-field
                      v-model="description"
                      :rules="textRules"
                      :counter="280"
                      label="Need description"
                      required
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    md="2"
                  >
                    <v-btn @click="submit">submit</v-btn>
                  </v-col>
                </v-row>
              </v-container>
            </v-form>
          </v-card-text>
        </v-card>
      </v-flex>
      <v-flex
        xs12
      >
        <v-card
          class="mx-auto my-3"
        >
          <v-card-title>2. List engineering aspects impacting each need</v-card-title>
          <v-card-text>
            <p class="text-left">Design parameters that can be controlled during the development. Value Drivers are the key engineering characteristics.</p>
            <ul>
              <li>Example</li>
              <li>Example 2</li>
            </ul>
          </v-card-text>
        </v-card>
      </v-flex>
      <v-flex
        xs12
      >
        <v-card
          class="mx-auto my-3"
        >
          <v-card-title>3. Specify a set of Value Creation Strategies</v-card-title>
          <v-card-text>
            <p class="text-left">Scenarios</p>
          </v-card-text>
        </v-card>
      </v-flex>
      <v-flex
        xs12
      >
        <v-card
          class="mx-auto my-3"
        >
          <v-card-title>4. Stablish priorities for a specific VCS</v-card-title>
          <v-card-text>
            <p class="text-left">Drag and drop the following needs to rank them so the ones you value the most are at the top:</p>
            <v-list flat>
              
              <v-list-item-group v-model="need" color="blue-grey">
                <draggable v-model="needs" group="needs" @end="updateNeedOrder">
                  <v-list-item
                    v-for="(need, i) in needs"
                    :key="i"
                  >
                    <v-list-item-icon>
                      <span v-text="need.order"></span>
                    </v-list-item-icon>
                    <v-list-item-content>
                      <v-list-item-title v-text="need.text"></v-list-item-title>
                    </v-list-item-content>
                    <v-list-item-icon>
                      <span v-text="need.icon"></span>
                    </v-list-item-icon>
                  </v-list-item>
                </draggable>
              </v-list-item-group>
            </v-list>
          </v-card-text>
        </v-card>
      </v-flex>
      <v-flex
        xs12
      >
        <v-card
          class="mx-auto my-3"
        >
          <v-card-title>5. Repeat for all VCSs</v-card-title>
          <v-card-text>
          </v-card-text>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import draggable from 'vuedraggable'
export default {
  components: {
    draggable,
  },
  data: () => ({
    valid: false,
    description: '',
    textRules: [
      v => !!v || 'This field is required',
      v => v.length <= 280 || 'Text must be less than 280 characters',
    ],
    need: null,
    needs: [
      { text: 'Low sale price', icon: '💰', order: '1' },
      { text: 'High performance', icon: '🏅', order: '2' },
      { text: 'High reliability', icon: '🐢', order: '3' },
      { text: 'High maintainability', icon: '🛠️', order: '4' },
    ],
  }),
  methods: {
    submit () {
      this.needs.push({ text: this.description, icon: "", order: this.needs.length + 1 })
      this.$refs.form.reset()
      this.description = ''
    },
    updateNeedOrder: function() {
      var needs = this.needs.map(function(need, index) {
        return { text: need.text, icon: need.icon, order: index+1 }
      })
      this.needs = needs
    },
  },
};
</script>
