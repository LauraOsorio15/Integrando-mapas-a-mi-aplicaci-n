# Integrando-mapas-a-mi-aplicaci-n
import android.content.Intent;
import android.os.Bundle;
import androidx.appcompat.app.AppCompatActivity;
import com.google.android.gms.maps.CameraUpdateFactory;
import com.google.android.gms.maps.GoogleMap;
import com.google.android.gms.maps.MapView;
import com.google.android.gms.maps.OnMapReadyCallback;
import com.google.android.gms.maps.model.LatLng;
import com.google.android.gms.maps.model.MarkerOptions;

public class MapActivity extends AppCompatActivity implements OnMapReadyCallback {

    private GoogleMap mMap;
    private MapView mMapView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_map);

        // Obtener el lugar seleccionado del intent
        Intent intent = getIntent();
        String lugarSeleccionado = intent.getStringExtra("LUGAR_SELECCIONADO");

        // Configurar el mapa
        mMapView = findViewById(R.id.mapView);
        if (mMapView != null) {
            mMapView.onCreate(null);
            mMapView.onResume();
            mMapView.getMapAsync(this);
        }
    }

    @Override
    public void onMapReady(GoogleMap googleMap) {
        mMap = googleMap;

        // Obtener la ubicación del lugar seleccionado (puedes usar ubicaciones ficticias aquí)
        LatLng lugarLatLng = new LatLng(0, 0);  // Latitud y longitud del lugar

        // Añadir un marcador personalizado
        mMap.addMarker(new MarkerOptions()
                .position(lugarLatLng)
                .title("Lugar Seleccionado")
                .snippet("Descripción del lugar"));

        // Mover la cámara al lugar seleccionado y establecer un nivel de zoom
        mMap.moveCamera(CameraUpdateFactory.newLatLngZoom(lugarLatLng, 15.0f));
    }
}
