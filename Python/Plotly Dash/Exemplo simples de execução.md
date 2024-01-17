```
from dash import Dash

from dash_html_components import H1

app = Dash(__name__)

app.layout = H1("Hello World")

app.run_server(debug=True)
```
