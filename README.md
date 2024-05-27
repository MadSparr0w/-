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
    public bool canPush;

    private void OnTriggerEnter(Collider other) 
    {
        if (canPush)
        {
            if (other.CompareTag("Cube") || other.CompareTag("Player")) #При условии, что кнопку коснулся обычный куб или игрок
            {
                foreach (GameObject first in firstGroup) #В этом случае выполняется цикл превращения с обычного на прозрачный
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
                button.canPush = true;
            }
        }
    }
}
