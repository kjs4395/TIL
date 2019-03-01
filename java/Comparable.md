# Comparable 
- 객체의 특정 속성을 가지고 정렬이 되도록 할때 (일반적인 정렬)
- CompareTo() 메소드 구현

~~~
public class Student implements Comparable<Student>{
    String name;
    Integer age;
    Integer grade;


    public Student(String name, Integer age, Integer grade) {
        this.name = name;
        this.age = age;
        this.grade = grade;
    }

    @Override
    public int compareTo(Student o) {
        // 나이 오름차순
        //return this.age - o.age;
        return o.age - this.age;
    }
    

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", grade=" + grade +
                '}';
    }
}

~~~

- 구현 후 정렬시 Arrays.sort() or Collections.sort()사용하면 자동 정렬

~~~
        Student student1 = new Student("jisun", 28, 3);
        Student student2 = new Student("dayoung", 2, 1);
        Student student3 = new Student("minhee", 24, 4);

        List<Student> students = new ArrayList<>();
        students.add(student1);
        students.add(student2);
        students.add(student3);

        Collections.sort(students);
~~~


# Comparator
- 객체 간의 특정한 정렬이 필요할때 사용
- Compare() 메소드 구현
- collections.sort()나 Arrays.sort()의 두번째 인자로 받아서 사용 가능

~~~
       Collections.sort(students, new Comparator<Student>() {
            @Override
            public int compare(Student o1, Student o2) {
                return o1.getName().compareTo(o2.getName());
            }
        });

        for(int i=0; i<students.size(); i++) {
            System.out.println(students.get(i).toString());
        }
~~~
