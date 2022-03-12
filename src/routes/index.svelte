<script lang="ts">
    import { Geolocation } from '@capacitor/geolocation'; // TODO: remove geolocation (unnecessary)
    let placeholderText: string = "Waiting...";

    let loc = undefined;
    const getCurrentPosition = async () => {
        await Geolocation.requestPermissions();
        const hasPermission: boolean = ( await Geolocation.checkPermissions() ).location == "granted";

        if ( hasPermission ) {
            placeholderText = "Getting...";
            loc = await Geolocation.getCurrentPosition();
        } else { placeholderText = "No geolocation permissions! :("; }
    }
</script>
  
<div>
    <h1>Geolocation</h1>
    <p>Your location is:</p>
    <p>Latitude: { loc?.coords.latitude ?? placeholderText }</p>
    <p>Longitude: { loc?.coords.longitude ?? placeholderText }</p>

    <button on:click={ getCurrentPosition }>
        Get Current Location
    </button>
</div>