========================
Le local est-il ouvert ?
========================

:slug: statut

.. raw:: html

    <p id="spaceapi_open_page">
        Pas en ce moment ; n’hésitez pas à consulter
        <a href="/pages/agenda.html">l’agenda</a> pour connaitre la prochaine
        ouverture du local !
    </p>
    <script type="text/javascript">
        $(document).ready(function() {
            $.getJSON("http://spaceapi.net/new/space/haum/status/json", function(data) {
                if (data.state.open)
                    $("#spaceapi_open_page").html('<img src="/theme/images/open.png">');
            });
        });
    </script>
