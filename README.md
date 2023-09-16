# pattern
#include <gtk/gtk.h>

// Callback function to draw the pattern
gboolean draw_pattern(GtkWidget *widget, cairo_t *cr, gpointer data) {
    GdkRGBA color;
    cairo_set_line_width(cr, 5);

    for (int i = 0; i < 10; i++) {
        gdk_rgba_parse(&color, "blue");
        cairo_set_source_rgba(cr, color.red, color.green, color.blue, 1.0);
        cairo_rectangle(cr, i * 30, i * 30, 150, 150);
        cairo_fill(cr);

        gdk_rgba_parse(&color, "red");
        cairo_set_source_rgba(cr, color.red, color.green, color.blue, 1.0);
        cairo_rectangle(cr, i * 30 + 5, i * 30 + 5, 140, 140);
        cairo_stroke(cr);
    }

    return FALSE;
}

int main(int argc, char *argv[]) {
    gtk_init(&argc, &argv);

    GtkWidget *window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
    gtk_window_set_title(GTK_WINDOW(window), "Cool Pattern");
    gtk_window_set_default_size(GTK_WINDOW(window), 400, 400);
    g_signal_connect(G_OBJECT(window), "destroy", G_CALLBACK(gtk_main_quit), NULL);

    GtkWidget *drawing_area = gtk_drawing_area_new();
    gtk_container_add(GTK_CONTAINER(window), drawing_area);
    g_signal_connect(G_OBJECT(drawing_area), "draw", G_CALLBACK(draw_pattern), NULL);

    gtk_widget_show_all(window);

    gtk_main();

    return 0;
}
