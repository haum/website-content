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
            $.get("/spacestatus", function(data) {
                if (data==1)
                    $("#spaceapi_open_page").html('<img src="/theme/images/open.png">');
            });
        });
    </script>
