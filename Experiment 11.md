{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "provenance": [],
      "authorship_tag": "ABX9TyNa3hKaDUVyjXh3ETLX0dda",
      "include_colab_link": true
    },
    "kernelspec": {
      "name": "python3",
      "display_name": "Python 3"
    },
    "language_info": {
      "name": "python"
    }
  },
  "cells": [
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "view-in-github",
        "colab_type": "text"
      },
      "source": [
        "<a href=\"https://colab.research.google.com/github/kowshik5063/CSA6301-Threat-Intelligence/blob/main/Experiment%2011.md\" target=\"_parent\"><img src=\"https://colab.research.google.com/assets/colab-badge.svg\" alt=\"Open In Colab\"/></a>"
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "from cryptography.fernet import Fernet\n",
        "\n",
        "key = Fernet.generate_key()\n",
        "cipher = Fernet(key)\n",
        "\n",
        "print(\"Shared Key:\", key.decode())\n",
        "\n",
        "message = b\"Transfer $500 to account 12345\"\n",
        "\n",
        "encrypted = cipher.encrypt(message)\n",
        "\n",
        "print(\"Encrypted message:\", encrypted)\n",
        "\n",
        "decrypted = cipher.decrypt(encrypted)\n",
        "\n",
        "print(\"Decrypted message:\", decrypted.decode())"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "NJuhg4DP-7hz",
        "outputId": "c3adf658-17df-4fa0-8b42-48ff3c89fead"
      },
      "execution_count": 5,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Shared Key: kdSNo_XS3F8LoUsp5zynwV_GoDNqCmHvfzzuDSs2IHs=\n",
            "Encrypted message: b'gAAAAABqkm2QERWP3D4aVLzQ8TuVlfLz8TdwAqG9IA5W7VG3UZ_HhPNLKlTAdTVRi2OUqJOU8O8ZKvkAe61IQXGOtJuKBxhmtjBeBfA5-JQpdu-am1AfbTU='\n",
            "Decrypted message: Transfer $500 to account 12345\n"
          ]
        }
      ]
    }
  ]
}