# JVM


public class JvmComprehension {

    public static void main(String[] args) <- в момент вызова метода создается фрейм(1) в Stack Memory, 
        
        int i = 1;                      // 1 <- Во фрейм сохраняется значение i=1;
        
        Object o = new Object();        // 2 <- new Object сохраняется в heap и ждет вызова, в Stack Memory "o" хранит ссылку на heap, где лежит new Object
        
        Integer ii = 2;                 // 3 <- сохраняет значние в heap
        
        printAll(o, i, ii);             // 4 <- Создает второй фрейм(2) в Stack Memory, происходит подругрузка классов, от Application ClassLoader > Platform ClassLoader > Bootstrap ClassLoader(Загрузил, если нашел) > Platform ClassLoader(Загрузил, если нашел)> Application ClassLoader(Загрузил, если нашел)
        
        
        System.out.println("finished"); // 7<- в третьем фрейме создается Sting со значением "finished"
    }

    private static void printAll(Object o, int i, Integer ii) { <- Находит в heap где лежит new Object и значение Integer ii
    
        Integer uselessVar = 700;                   // 5 <- сохраняет значние в heap, далее это нигде не используется, сборщик мусора это находи и удаляет.
        
        System.out.println(o.toString() + i + ii);  // 6 <- Cоздается новый фрейм (3) в Stack Memory, куда передается i и ссылка на "ii" и "o"
    }
}
