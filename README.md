<?php
class Quiz {
    public $questions = [
        ["q" => "What is the capital of France?", "a" => "Paris"],
        ["q" => "2 + 2 = ?", "a" => "4"],
        ["q" => "What color is the sky?", "a" => "Blue"]
    ];

    public function score($answers) {
        $score = 0;
        foreach ($this->questions as $i => $q) {
            if (strtolower($answers["answer$i"]) === strtolower($q["a"])) {
                $score++;
            }
        }
        return $score;
    }
}

$quiz = new Quiz();
$score = null;

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $score = $quiz->score($_POST);
}
?>
<!DOCTYPE html>
<html>
<head>
    <title>Professional PHP Quiz</title>
    <style>body{font-family:Arial;margin:50px;}</style>
</head>
<body>
    <h2>PHP Quiz Game</h2>
    <form method="post">
        <?php foreach($quiz->questions as $i => $q): ?>
            <p><?= $q["q"] ?></p>
            <input type="text" name="answer<?= $i ?>" required><br>
        <?php endforeach; ?>
        <button type="submit">Submit</button>
    </form>
    <?php if(!is_null($score)): ?>
        <h3>Your Score: <?= $score ?>/<?= count($quiz->questions) ?></h3>
    <?php endif; ?>
</body>
</html>
