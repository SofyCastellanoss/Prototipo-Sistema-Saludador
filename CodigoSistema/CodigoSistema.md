##Codigo de la lógica del sistema saludador

import javafx.application.Application;
import javafx.geometry.Insets;
import javafx.geometry.Pos;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.control.ComboBox;
import javafx.scene.control.Label;
import javafx.scene.control.Spinner;
import javafx.scene.control.TextField;
import javafx.scene.layout.HBox;
import javafx.scene.layout.StackPane;
import javafx.scene.layout.VBox;
import javafx.scene.text.TextAlignment;
import javafx.stage.Stage;

public class SistemaSaludador extends Application {

    private VBox panelInicio;
    private VBox panelFormulario;
    private VBox panelResultado;

    private TextField campoNombre;
    private Spinner<Integer> spinnerEdad;
    private TextField campoHora;
    private ComboBox<String> comboAmPm;
    private Label etiquetaError;
    private Label etiquetaSaludo;
    private Label etiquetaDetalle;

    @Override
    public void start(Stage stage) {
        panelInicio = crearInicio();
        panelFormulario = crearFormulario();
        panelResultado = crearResultado();

        StackPane raiz = new StackPane(panelInicio, panelFormulario, panelResultado);
        raiz.setPadding(new Insets(32));
        raiz.setStyle("-fx-background-color: linear-gradient(to bottom right, #ecfeff, #e0f2fe, #f0fdf4);");

        mostrar(panelInicio);

        stage.setTitle("Sistema Saludador");
        stage.setScene(new Scene(raiz, 680, 540));
        stage.show();
    }

    private VBox crearInicio() {
        Label titulo = new Label("Sistema Saludador");
        titulo.setStyle("-fx-font-size: 28px; -fx-font-weight: bold; -fx-text-fill: #0f766e;");

        Label texto = new Label("El estudiante solicita un saludo y el sistema responde con su nombre y su edad.");
        texto.setWrapText(true);
        texto.setStyle("-fx-font-size: 15px; -fx-text-fill: #475569;");

        Button solicitar = new Button("Solicitar saludo");
        estiloPrincipal(solicitar);
        solicitar.setOnAction(e -> {
            limpiarFormulario();
            mostrar(panelFormulario);
            campoNombre.requestFocus();
        });

        VBox caja = tarjeta(titulo, texto, solicitar);
        caja.setAlignment(Pos.CENTER);
        return caja;
    }

    private VBox crearFormulario() {
        Label titulo = new Label("Datos del estudiante");
        titulo.setStyle("-fx-font-size: 28px; -fx-font-weight: bold; -fx-text-fill: #0f766e;");

        Label texto = new Label("El sistema solicita nombre, edad, hora y si es AM o PM.");
        texto.setWrapText(true);
        texto.setStyle("-fx-font-size: 15px; -fx-text-fill: #475569;");

        campoNombre = new TextField();
        campoNombre.setPromptText("Ej. Sofía");

        spinnerEdad = new Spinner<>(1, 120, 18);
        spinnerEdad.setEditable(true);
        spinnerEdad.setPrefWidth(160);

        campoHora = new TextField();
        campoHora.setPromptText("hh:mm  (ej. 10:30)");
        campoHora.setPrefWidth(220);

        comboAmPm = new ComboBox<>();
        comboAmPm.getItems().addAll("AM", "PM");
        comboAmPm.setValue("AM");
        comboAmPm.setPrefWidth(110);

        HBox filaHora = new HBox(10, campoHora, comboAmPm);
        filaHora.setAlignment(Pos.CENTER_LEFT);

        etiquetaError = new Label();
        etiquetaError.setWrapText(true);
        etiquetaError.setStyle("-fx-text-fill: #b91c1c;");

        Button volver = new Button("Volver");
        estiloSecundario(volver);
        volver.setOnAction(e -> mostrar(panelInicio));

        Button confirmar = new Button("Confirmar");
        estiloPrincipal(confirmar);
        confirmar.setOnAction(e -> confirmarDatos());

        HBox botones = new HBox(12, volver, confirmar);
        botones.setAlignment(Pos.CENTER_RIGHT);

        VBox caja = tarjeta(
                titulo, texto,
                etiqueta("Nombre"), campoNombre,
                etiqueta("Edad"), spinnerEdad,
                etiqueta("Hora (12 h) y AM/PM"), filaHora,
                etiquetaError, botones
        );
        caja.setAlignment(Pos.TOP_LEFT);
        return caja;
    }

    private VBox crearResultado() {
        Label titulo = new Label("Saludo");
        titulo.setStyle("-fx-font-size: 28px; -fx-font-weight: bold; -fx-text-fill: #0f766e;");

        etiquetaSaludo = new Label();
        etiquetaSaludo.setWrapText(true);
        etiquetaSaludo.setTextAlignment(TextAlignment.CENTER);
        etiquetaSaludo.setStyle("-fx-font-size: 24px; -fx-font-weight: bold;");

        etiquetaDetalle = new Label();
        etiquetaDetalle.setWrapText(true);
        etiquetaDetalle.setTextAlignment(TextAlignment.CENTER);
        etiquetaDetalle.setStyle("-fx-font-size: 16px; -fx-text-fill: #475569;");

        Button otro = new Button("Otro saludo");
        estiloPrincipal(otro);
        otro.setOnAction(e -> {
            limpiarFormulario();
            mostrar(panelFormulario);
            campoNombre.requestFocus();
        });

        Button inicio = new Button("Inicio");
        estiloSecundario(inicio);
        inicio.setOnAction(e -> mostrar(panelInicio));

        HBox botones = new HBox(12, otro, inicio);
        botones.setAlignment(Pos.CENTER);

        VBox caja = tarjeta(titulo, etiquetaSaludo, etiquetaDetalle, botones);
        caja.setAlignment(Pos.CENTER);
        return caja;
    }

    private void confirmarDatos() {
        etiquetaError.setText("");
        spinnerEdad.commitValue();

        String nombre = campoNombre.getText() == null ? "" : campoNombre.getText().trim();
        Integer edad = spinnerEdad.getValue();
        String horaTexto = campoHora.getText() == null ? "" : campoHora.getText().trim();
        String amPm = comboAmPm.getValue();

        if (nombre.length() < 2) {
            etiquetaError.setText("Escribe tu nombre (mínimo 2 caracteres).");
            return;
        }
        if (edad == null || edad < 1 || edad > 120) {
            etiquetaError.setText("La edad debe estar entre 1 y 120 años.");
            return;
        }
        if (!horaTexto.matches("\\d{1,2}[:.]\\d{2}")) {
            etiquetaError.setText("Ingresa la hora en formato hh:mm (ejemplo: 10:30).");
            return;
        }
        if (amPm == null) {
            etiquetaError.setText("Selecciona AM o PM.");
            return;
        }

        String[] partes = horaTexto.split("[:.]");
        int hora12 = Integer.parseInt(partes[0]);
        int minutos = Integer.parseInt(partes[1]);
        if (hora12 < 1 || hora12 > 12 || minutos < 0 || minutos > 59) {
            etiquetaError.setText("La hora debe estar entre 1 y 12, y los minutos entre 00 y 59.");
            return;
        }

        int hora24;
        if ("AM".equals(amPm)) {
            hora24 = hora12 == 12 ? 0 : hora12;
        } else {
            hora24 = hora12 == 12 ? 12 : hora12 + 12;
        }

        String momento;
        if (hora24 >= 5 && hora24 < 12) {
            momento = "¡Buenos días";
        } else if (hora24 >= 12 && hora24 < 19) {
            momento = "¡Buenas tardes";
        } else {
            momento = "¡Buenas noches";
        }

        String anios = edad == 1 ? "año" : "años";
        etiquetaSaludo.setText(momento + ", " + nombre + ".");
        etiquetaDetalle.setText("Tienes " + edad + " " + anios + ".");
        mostrar(panelResultado);
    }

    private void mostrar(VBox visible) {
        panelInicio.setVisible(visible == panelInicio);
        panelInicio.setManaged(visible == panelInicio);
        panelFormulario.setVisible(visible == panelFormulario);
        panelFormulario.setManaged(visible == panelFormulario);
        panelResultado.setVisible(visible == panelResultado);
        panelResultado.setManaged(visible == panelResultado);
    }

    private void limpiarFormulario() {
        campoNombre.clear();
        spinnerEdad.getValueFactory().setValue(18);
        campoHora.clear();
        comboAmPm.setValue("AM");
        etiquetaError.setText("");
    }

    private static VBox tarjeta(javafx.scene.Node... nodos) {
        VBox caja = new VBox(14, nodos);
        caja.setMaxWidth(520);
        caja.setPadding(new Insets(36));
        caja.setStyle(
                "-fx-background-color: white; -fx-background-radius: 20; " +
                "-fx-effect: dropshadow(gaussian, rgba(15,23,42,0.12), 24, 0.2, 0, 8);"
        );
        return caja;
    }

    private static Label etiqueta(String texto) {
        Label label = new Label(texto);
        label.setStyle("-fx-font-size: 13px; -fx-font-weight: bold; -fx-text-fill: #334155;");
        return label;
    }

    private static void estiloPrincipal(Button boton) {
        boton.setStyle(
                "-fx-background-color: #0d9488; -fx-text-fill: white; -fx-font-size: 15px; " +
                "-fx-font-weight: bold; -fx-background-radius: 12; -fx-padding: 10 22;"
        );
    }

    private static void estiloSecundario(Button boton) {
        boton.setStyle(
                "-fx-background-color: #e2e8f0; -fx-text-fill: #334155; " +
                "-fx-font-size: 14px; -fx-background-radius: 12; -fx-padding: 10 18;"
        );
    }

    public static void main(String[] args) {
        launch(args);
    }
}
