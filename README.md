

    using System.Collections;
    using System.Collections.Generic;
    using UnityEngine;

    public class Activator : MonoBehaviour
    {
        public GameObject[] firstGroup; #массивы 2-х групп
        public GameObject[] secondGroup; 
        public Activator button;
        public Material normal; #Переключение с нормального на прозрачный
        public Material transparent; 
        public bool canPush; #новый класс
        private void OnTriggerEnter(Collider other) 
        {
            if (canPush)
            {
                if (other.CompareTag("Cube") || other.CompareTag("Player")) #Приусловии,чтокнопкукоснулсяобычныйкубилиигрок
                {
                    foreach (GameObject first in firstGroup) #Вэтомслучаевыполняетсяциклпревращениясобычногонапрозрачный
                    {
                        first.GetComponent<Renderer>().material = normal; #И наоборот
                        first.GetComponent<Collider>().isTrigger = false;
                    }
                    foreach (GameObject second in secondGroup)
                    {
                        second.GetComponent<Renderer>().material = transparent; 
                        second.GetComponent<Collider>().isTrigger = true;
                    }
                    GetComponent<Renderer>().material = transparent;
                    button.GetComponent<Renderer>().material = normal;
                    button.canPush = true; #При соблюдении условия (если в кубе ничего нет то кнопка может быть нажата)
                }
            }
        }
    }
