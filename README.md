# 27PR
# 27 Практика
# Задание 1-3
```
import java.util.LinkedList;

class HashTable {
    private static class Entry {
        String key;
        String value;

        Entry(String key, String value) {
            this.key = key;
            this.value = value;
        }
    }

    private LinkedList<Entry>[] table;
    private int size;

    public HashTable(int size) {
        this.size = size;
        table = new LinkedList[size];
        for (int i = 0; i < size; i++) {
            table[i] = new LinkedList<>();
        }
    }

    private int hash(String key) {
        return Math.abs(key.hashCode()) % size;
    }

    public void add(String key, String value) {
        int index = hash(key);
        for (Entry entry : table[index]) {
            if (entry.key.equals(key)) {
                entry.value = value; // Обновляем значение, если ключ существует
                return;
            }
        }
        table[index].add(new Entry(key, value)); // Добавляем новый элемент
    }

    public String lookup(String key) {
        int index = hash(key);
        for (Entry entry : table[index]) {
            if (entry.key.equals(key)) {
                return entry.value; // Возвращаем значение
            }
        }
        return null; // Не найдено
    }

    public void delete(String key) {
        int index = hash(key);
        table[index].removeIf(entry -> entry.key.equals(key)); // Удаляем элемент по ключу
    }
}

public class Main {
    public static void main(String[] args) {
        HashTable hashTable = new HashTable(10);

        hashTable.add("key1", "value1");
        hashTable.add("key2", "value2");
        hashTable.add("key3", "value3");
        hashTable.add("key4", "value4");
        hashTable.add("key5", "value5");
        hashTable.add("key6", "value6");
        hashTable.add("key7", "value7");
        hashTable.add("key8", "value8");
        hashTable.add("key9", "value9");
        hashTable.add("key10", "value10");

        String valueToLookup = hashTable.lookup("key5");
        if (valueToLookup != null) {
            System.out.println("Найдено: key5 -> " + valueToLookup);
        } else {
            System.out.println("Ключ не найден.");
        }

        hashTable.delete("key5");
        valueToLookup = hashTable.lookup("key5");
        if (valueToLookup == null) {
            System.out.println("key5 успешно удален.");
        }
    }
}
```
