<template>
    <div>
        <SearchBar @termChange="onTermChange"></SearchBar>
        <VideoList></VideoList>   
        {{ videos.length }}
    </div> 
</template>

<script>
import axios from "axios";
import SearchBar from './components/SearchBar';
import VideoList from './components/VideoList';

const API_KEY = 'AIzaSyDQYr_yoDIHWj5pdsl44L1xUhS_YlXoOZ4';

export default {
    name: 'App',
    components: { 
        SearchBar: SearchBar,
        VideoList: VideoList
    },
    data(){
        return { videos: [] };
    },
    methods: {
        onTermChange: function(searchText) {
            
            axios.get('https://www.googleapis.com/youtube/v3/search', {
                params: {
                    key: API_KEY,
                    type: 'video',
                    part: 'snippet',
                    q: searchText
                }
            }).then(resp => {
                this.videos = resp.data.items;
            });
        }        
    }   
};
</script>