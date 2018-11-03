<template>
    <Page>
        <ActionBar flat="true">
            <StackLayout orientation="horizontal">
                <Label text="Gate" fontSize="32" verticalAlignment="center" />
            </StackLayout>
        </ActionBar>

        <StackLayout>
            <Image src="res://logo" width="200" height="200" stretch="aspectFit" />
            <Button text="Lock" @tap = "onLockTap" />
            <Button text="Unlock" @tap = "onUnlockTap" /> 
        </StackLayout>
    </Page>
</template>

<script>
import axios from 'axios';

const baseUrl = 'https://api.particle.io/v1/devices/2c0045000a47363339343638';
const token = '0860c9c60a8172eb71a999889017f37eb611b576';

const callParticleAPI = (endpoint, value) => {
  axios({
    method: 'POST',
    url: `${baseUrl}/${endpoint}?access_token=${token}`,
    data: `{ "args": "${value}" }`,
    headers: { 'content-type': 'application/json' }
  }).catch(error => {
    console.error(error);
  });
};
 export default {
  data() {
    return {
        lock: '',
        unlock: '',
     //   url: ''
  };
},
    methods: {
        onLockTap: function(args) {
        callParticleAPI('runMotor', 'lock');
        console.log("Locked");
    },
        onUnlockTap: function(args) {
        callParticleAPI('runMotor', 'unlock');
        console.log("Unlocked");
     }
    }
};
</script>

<style scoped>
    ActionBar {
        background-color: #ffffff;
        color: #000000;
    }

    .message {
        vertical-align: center;
        text-align: center;
        font-size: 20;
        color: #333333;
    }
</style>
