
when entering <script> alert("XSS") </script>
??? Sorry, we don't have that movie :("}]}'; // var JSONResponse = eval ("(" + JSONResponseString + ")"); var JSONResponse = JSON.parse(JSONResponseString); document.getElementById("result").innerHTML=JSONResponse.movies[0].response

<script>

        var JSONResponseString = '{"movies":[{"response":"<script> alert("XSS")</script>??? Sorry, we don&#039;t have that movie :("}]}';
        // var JSONResponse = eval ("(" + JSONResponseString + ")");
        var JSONResponse = JSON.parse(JSONResponseString);
        document.getElementById("result").innerHTML=JSONResponse.movies[0].response;

    </script>

("}]}';alert("XSS")</script>

