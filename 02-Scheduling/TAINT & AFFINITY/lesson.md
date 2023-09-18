Dependendo da situação, mas por norma estes dois deviam trabalhar em conjunto

- Enquanto com o **taint and toleration** aquilo que fazemos é por uma barra protetora no node, isto é dizemos que o node tem uma label color=red o que quer dizer que caso um pod que não tenha essa label o scheduler ao tentar colocar esse pod nesse node vai ser barrado porque só entra naquele node quem tiver a label igual a color=red.
Qual é a única coisa que este metodo não garante? é que mesmo que o node tenha a mesma label que o pod não é garantido que o pod vá para esse node, mesmo que o pod tenha a label ex: color=red ele pode ser colocado num node sem labels, mas não será colocado num node com label color=blue.

- Enquanto o affinity é ao contrário, isto é, pomos uma label de color=red e no pod pomos a affinity color=red o sheduler vai por o pod no node que tiver a mesma label, caso não haja nenhum node com a mesma label que o pod, o pod não é executado. Com o affinity garantimos que um pod com a mesma label que o node ele vai ser colocado lá. 
Qual é a única coisa que este método não garante? é que um pod "neutro" que não tenha label também pode ser colocado num node com label. Este metodo não garante que só pod com labels é que são colcoados nesses node. O que garante é que aquele respetivo pod vai para o node que tenha a mesma label.

- Agora dependendo das situações e perante o que queremos fazer podemos usar um método ou outro, mas caso queirámos que determinados pods sejam colocados dentro de um determinado node sem outros pods "neutros" então aí utilizámos os dois métodos.

- Taint garante que não entrem pods neutros e o affinity garante que aquele pod vai para aquele determinado node.