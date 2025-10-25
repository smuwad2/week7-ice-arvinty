<script>
import axios from 'axios';

export default { 
    data() {
        return {
            moods: ["Happy", "Sad", "Angry"],
            subject: "",
            entry: "",
            mood: "",
            outputMsg: "",
        }
    },
    computed: {
        baseUrl() {
            if (window.location.hostname === 'localhost')
                return 'http://localhost:3000' 
            else {
                const codespace_host = window.location.hostname.replace('5173', '3000')
                return `https://${codespace_host}`;
            }
        }
    },
    methods: {
        addPost() {
            // Validate inputs
            if (!this.subject || !this.entry || !this.mood) {
                this.outputMsg = "Please fill in all fields";
                return;
            }

            axios.get(`${this.baseUrl}/addPost`, {
                params: {
                    'subject': this.subject,
                    'entry': this.entry,
                    'mood': this.mood,
                }
            }).then(response => {
                this.outputMsg = response.data.message;
                // Optional: Clear form after successful submission
                // this.subject = "";
                // this.entry = "";
                // this.mood = "";
            }).catch(error => { 
                console.log(error);
                this.outputMsg = "Error: " + error.message;
            })
        }
    }
}
</script>

<template>
    <div class="table m-2">
        <h3>Add a New Blog Post</h3>

        Subject: <input type='text' size='30' v-model='subject' required>
        <br>

        Entry: <br>
        <textarea name='entry' cols='80' rows='5' v-model='entry' required></textarea>
        <br>

        Mood:
        <select v-model="mood">
            <option value="">-- Select a mood --</option>
            <option v-for="moodOption in moods" :key="moodOption" :value="moodOption">
                {{ moodOption }}
            </option>
        </select>
        <br>

        <br>
        <button @click="addPost()">Submit New Post</button>
        <br>
        {{ outputMsg }}
        <hr> 
        Click <router-link to="/ViewPosts/">here</router-link> to return to Main Page
    </div>
</template>